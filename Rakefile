# encoding: utf-8
desc "FuelPHPで作るWEBアプリケーションのボイラープレート作成"
task :default do

  projectname = "sandbox"
  sh "git clone --recursive git://github.com/fuel/fuel.git #{projectname}"
  cd projectname

  submodules = []
  pair = {}
  open('.gitmodules', 'r').each do |line|
    if /path = (.*)$/.match(line) then
      pair[:path] = $1
    elsif /url = (.*)$/.match(line) then
      pair[:url] = $1
      submodules.push(pair)
      pair = {}
    end
  end

  del_files = ["CHANGELOG.md", "CONTRIBUTING.md", "README.md", "TESTING.md", ".gitmodules"]
  rm del_files

  del_dirs = ['.git', 'docs/']
  sh "sudo rm -R #{del_dirs.join(' ')}"

  sh "git init"
  submodules.each do |mod|
    sh "git submodule add #{mod[:url]} #{mod[:path]}"
  end

  rm "fuel/app/config/config.php"
  cp "fuel/core/config/config.php", "fuel/app/config/config.php"

end

#$ rm CHANGELOG.md CONTRIBUTING.md README.md TESTING.md .gitmodules
#$ sudo rm -R .git docs/
#$ git init
#$ git submodule add git://github.com/fuel/core.git fuel/core
#$ git submodule add git://github.com/fuel/auth.git fuel/packages/auth
#$ git submodule add git://github.com/fuel/email.git fuel/packages/email
#$ git submodule add git://github.com/fuel/oil.git fuel/packages/oil
#$ git submodule add git://github.com/fuel/orm.git fuel/packages/orm
#$ git submodule add git://github.com/fuel/parser.git fuel/packages/parser
#$ rm fuel/app/config/config.php
#$ cp fuel/core/config/config.php fuel/app/config/config.php
#// set line 104 of the config file to the correct timezone
#$ git add .
#$ git commit -m "Initial commit"
