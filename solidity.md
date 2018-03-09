- https://remix.ethereum.org/
- http://solidity.readthedocs.io/en/develop/introduction-to-smart-contracts.html
- no floating-point arithmetic
- uint

Unit	| Wei | Value	Wei
--|---|--
wei	|1 wei|	1
Kwei (babbage)	|1e3 wei|	1,000
Mwei (lovelace)	|1e6 wei|	1,000,000
Gwei (shannon)	|1e9 wei|	1,000,000,000
microether (szabo)	|1e12 wei|	1,000,000,000,000
milliether (finney)	|1e15 wei|	1,000,000,000,000,000
ether	|1e18 wei|	1,000,000,000,000,000,000
- now ?
- error handling
  * revert()
  * assert(bool): use up all gas, donate ether to miners
    + `assert(nextPayday < now)`
  * require(bool)
    + `require(msg.sender == owner)`
- Array
  * fix length: `uint[5] a`
  * Dynamically-sized: `uint[] a`
    + `a.push(1)`
- mapping
  * key (bool, int, address, string), only these 4 type can be a map key
  * value (any type)
  * hash function: keccak256hash
  * use storage memory
  * **cannot loop the map**
  * employees[key]=value
  * value = employees[key]
    + value is a reference to storage memory
    + when key does not exist, value = type's default
- struct
  ```
  struct Employee{
    address id;
    uint salary;
    uint lastPayday;
  }
  Employee[] employees;
  employees.push(Employee(id, salary, now));
  ```
- for loop
  ```
  for (uint i = 0; i < employees.length; i++){
    if (employees[i].id == employee){
      delete employees[i];
      employees[i] = employees[employees.length - 1];
      employees.length -= 1;
      return;
    }
  }
  ```
- delete
  * `delete employees[0]`
- visibility
  * function
    + public(default)
    + external:
      ```
      function func1() external{

      }
      function func2(){
        func1(); // error
      }
      function func3(){
        this.func1(); // ok
      }
      ```
    + internal: like java protected keyword, visible to subclass
    + private
  * member variable
    + only public, internal, private(default)
      - public will create getter function automatically
      - `uint public a`
      - `mapping(uint => uint) public a;`
- Data location
  * storage
    + the default for local variables is storage
    + the location is forced to storage for state variables
  * memory
    + default for function parameters (including return parameters)
  * calldata: non-modifiable, non-persistent
- Forced data location:
  * parameters (not return) of external functions: calldata
  * state variables: storage
- Default data location:
  * parameters (also return) of functions: memory
  * all other local variables: storage
https://ethereum.stackexchange.com/questions/25554/can-anyone-explain-the-meaning-of-local-variable-and-state-variable-and-the-dif
- storage memory variable assignment
- [function modifiers](https://ethereum.stackexchange.com/questions/25200/solidity-what-is-the-difference-between-view-and-constant)
  * constant: constant function should not modify the state (not fully enforced yet)
  * the keyword view is introduced for functions (it replaces constant). Calling a view cannot alter the behaviour of future interactions with any contract. This means such functions **cannot use SSTORE**, **cannot send or receive ether** and can only call other view or pure functions.
  * the keyword pure is introduced for functions, they are view functions with the additional restriction that **their value only depends on the function arguments**. This means they cannot use SSTORE, SLOAD, cannot send or receive ether, **cannot use msg or block** and can only call other pure functions.
  * the keyword constant is invalid on functions
  * the keyword constant on any variable means it cannot be modified (and could be placed into memory or bytecode by the optimiser)
- named return value
  * `returns (uint salary, uint lastPayday)`
  * no need to explicitly `return` inside function
- solidity multiple inheritance
  * Method Resolution Order use [C3 Linearization](https://en.wikipedia.org/wiki/C3_linearization)
- modifier
  ```
  modifier onlyOwner{
    // _; // execute after method
    require(msg.sender == owner);
    _; // execute before method
  }
  ```
- use library https://github.com/OpenZeppelin/zeppelin-solidity
  * Safe math
    ```
    import './SafeMath.sol';
    using SafeMath for uint8;
    uint8 public a = 101;
    function test(){
      a = a.sub(100);
    }
    ```


- tx.origin v.s. msg.sender
  * http://vessenes.com/tx-origin-and-ethereum-oh-my/


- fallback function
  * http://solidity.readthedocs.io/en/develop/types.html#members-of-addresses

```solidity
pragma solidity ^0.4.14;

contract Payroll {
    uint constant payDuration = 10 seconds;

    uint totalSalary;

    address owner;
    struct Employee{
        address id;
        uint salary;
        uint lastPayday;
    }

    Employee[] employees;

    function Payroll() public{
        owner = msg.sender;
    }

    function _findEmployee(address e) private returns (Employee, uint){
        for (uint i = 0; i < employees.length; i++){
            if (employees[i].id == e){
                return (employees[i], i);
            }
        }
    }

    function _partialPaid(Employee employee) private{
        uint payment = employee.salary * (now - employee.lastPayday) / payDuration;
        employee.id.transfer(payment);
    }

    function addEmployee(address e, uint s) public{
        require(msg.sender == owner);
        var (employee, index) = _findEmployee(e);
        // when no employee is found, does _findEmployee return empty values?
        assert(employee.id == 0x0);
        employees.push(Employee(e, s * 1 ether, now));
        totalSalary += s;
    }

    function removeEmployee(address e) public{
        require(msg.sender == owner);
        var (employee, index) = _findEmployee(e);
        assert(employee.id != 0x0);
        _partialPaid(employee);
        totalSalary -= employee.salary;
        delete employees[index];
        employees[index] = employees[employees.length - 1];
        employees.length -= 1;
    }

    function updateEmployee(address e, uint s) public{
        require(msg.sender == owner);
        var (employee, index) = _findEmployee(e);
        assert(employee.id != 0x0);
        _partialPaid(employee);
        totalSalary -= employee.salary;
        employees[index].salary = s * 1 ether;
        employees[index].lastPayday = now;
        totalSalary += s;
    }

    function addFund() payable public returns (uint) {
        return this.balance;
    }

    function calculateRunway() public returns (uint){
        // uint totalSalary;
        // for (uint i = 0; i < employees.length; i++){
        //     totalSalary += employees[i].salary;
        // }
        return this.balance / totalSalary;
    }

    function hasEnoughFund() public returns (bool) {
        return calculateRunway() > 0;
    }

    function getPaid() public{
        var (employee, index) = _findEmployee(msg.sender);
        assert(employee.id != 0x0);

        uint nextPayday = employee.lastPayday + payDuration;
        assert(nextPayday < now);

        employees[index].lastPayday = nextPayday;
        employees[index].id.transfer(employee.salary);
    }
}
```
