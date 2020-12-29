https://docs.python-guide.org/dev/virtualenvs/#virtualenvironments-ref
https://www.ianmaddaus.com/post/manage-multiple-versions-python-mac/

Python'un son versiyonunu kurmak için
$ brew install python

brew yoksa kurmak için
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

$ python3 --version

$ pip --version

pip yoksa pip3 denenmeli

pip3'ün nerede olduğunu bulmak için:
$ which pip3

$ pip install --upgrade pip

direkt pip kullanılamaz ise bu da kullanılabilir.
$ python -m pip install [package_name]

pip yoksa pip3'ü refere etmesi için pip'in symlinki PATH'e eklenir. 
(kullanıcı home directory altındaki .zshrc dosyasına)
PATH="$PATH:/usr/local/opt/python@3.9/libexec/bin"

To update version of Python 3 (SORUN ÇIKARDI ALTA BAK !)
$ brew update
$ brew upgrade python3

brew ile kurulu package listesini verir.
$ brew list --versions

## Installing Pipenv
> Pipenv is a dependency manager for Python projects like Node.js’ npm.
$ pip install --user pipenv

Projeje dosyasına girilir.
$ cd project_folder

Bir paket kurmak için
$ pipenv install [package_name]
> The Pipfile is used to track which dependencies your project needs in case you need to re-install them, such as when you share your project with others. 

Programı çalıştırmak için
$ pipenv run python main.py

Kurulu paketleri görmek için
$ pipenv run pip freeze

Örneğin flask paketini kuralım
$ pipenv install flask
$ pipenv run python -c "import flask; print(flask.__version__)"
-c python kodu çalıştırır, örneğin flask'in versiyonunu gördük

Flask uses the Jinja template engine to dynamically build HTML pages

KURULUMDAN SONRA YAZAN BİLGİ
######################################
Python has been installed as
  /usr/local/bin/python3

Unversioned symlinks `python`, `python-config`, `pip` etc. pointing to
`python3`, `python3-config`, `pip3` etc., respectively, have been installed into
  /usr/local/opt/python@3.9/libexec/bin

You can install Python packages with
  pip3 install <package>
They will install into the site-package directory
  /usr/local/lib/python3.9/site-packages

See: https://docs.brew.sh/Homebrew-and-Python
==> Summary
🍺  /usr/local/Cellar/python@3.9/3.9.1_2: 3,895 files, 63.9MB
##################################################

## python'u upgrade ettiğimde yine eski versiyona refere etti. ÇÖZÜM:
https://stackoverflow.com/questions/46179672/python-bash-usr-local-bin-python-no-such-file-or-directory

Something seems to go haywire with Homebrew 1.7.2 and MacOS 10.13.6.

Even after removing all python versions and reinstalling, python --version simply won't work.

Most have probably already tried these steps...

brew uninstall --ignore-dependencies python
brew uninstall --ignore-dependencies python2
brew uninstall --ignore-dependencies python3
brew install python
brew unlink python && brew link python
brew unlink python3 && brew link python3

At the end what worked for me was...

sudo ln -s /usr/local/bin/python3 /usr/local/bin/python

And then again for pip...

sudo ln -s /usr/local/bin/pip3 /usr/local/bin/pip

OLDU...
########################################