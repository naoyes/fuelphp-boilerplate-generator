# encoding: utf-8
desc "FuelPHPで作るWEBアプリケーションのボイラープレート作成"
task :generate_fuelphp_boilerplate do
  projectname = "sandbox"
  sh "git clone --recursive git://github.com/fuel/fuel.git #{projectname}"
  cd projectname
  submodules = [ # .gitmodules から自動生成できるようにしたい
    {path:'fuel/core', url:'git://github.com/fuel/core.git'},
    {path:'fuel/packages/orm', url:'git://github.com/fuel/orm.git'},
    {path:'fuel/packages/auth', url:'git://github.com/fuel/auth.git'},
    {path:'fuel/packages/oil', url:'git://github.com/fuel/oil.git'},
    {path:'fuel/packages/parser', url:'git://github.com/fuel/parser.git'},
    {path:'fuel/packages/email', url:'git://github.com/fuel/email.git'},
  ]
  del_files = ["CHANGELOG.md", "CONTRIBUTING.md", "README.md", "TESTING.md", ".gitmodules"]
  rm del_files
  del_dirs = ['.git', 'docs/']
  sh "sudo rm -R #{del_dirs.join(' ')}"
  sh "git init"
  submodules.each do |mod|
    sh "git submodule add #{mod[:url]} #{mod[:path]}"
  end
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
