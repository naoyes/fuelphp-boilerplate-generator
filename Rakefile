# encoding: utf-8
desc "FuelPHPで作るWEBアプリケーションのボイラープレート作成"
task :default do

  appname = ENV['appname']
  sh "git clone --recursive git://github.com/fuel/fuel.git #{appname}"
  cd appname

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

  conf_file = 'fuel/app/config/config.php'
  rm conf_file
  cp "fuel/core/config/config.php", conf_file

  tz = "Asia/Tokyo"
  buff_file = 'fuel/app/config/config.php.buff'
  open(conf_file, 'r') do |f|
    open(buff_file, 'w') do |o|
      while line = f.gets
        line.gsub!("\'default_timezone\'   => null,", "\'default_timezone\'   => \'#{tz}\',")
        o.puts line
      end
    end
  end
  mv buff_file, conf_file

  sh "git add ."
  sh "git commit -m 'Initial commit'"
end
