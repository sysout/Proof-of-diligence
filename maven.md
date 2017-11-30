## run a single test
```bash
mvn test -DfailIfNoTests=false -Dtest=SomeTest -pl subproject
# if the subproject depends on other modules, then:
mvn test -DfailIfNoTests=false -Dtest=SomeTest -am
```
References.. 
* -am will make all the other sub-modules.
* -DfailIfNoTests=false does not fail the entire process since we are not intending to run tests in other modules.
* -pl option is not needed since -am is already building everything
