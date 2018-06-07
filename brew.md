## ENVIRONMENT
- HOMEBREW_NO_AUTO_UPDATE: If set, Homebrew will not auto-update before running `brew install`, `brew upgrade` or `brew tap`.

## install specific version
- [How to install apache-spark 2.2.0 with homebrew on Mac](https://stackoverflow.com/questions/49808951/how-to-install-apache-spark-2-2-0-with-homebrew-on-mac)
```bash
cd "$(brew --repo homebrew/core)"
git log Formula/apache-spark.rb
git checkout -b  apache-spark-2.2.0 bdf68bd79ebd16a70b7a747e027afbe5831f9cc3
brew unlink apache-spark
HOMEBREW_NO_AUTO_UPDATE=1 brew install apache-spark
# Cleanup
git checkout master
git branch -d apache-spark-2.2.0
# Check / switch
brew list apache-spark --versions
brew switch apache-spark 2.2.0
```
