# encoding: utf-8
desc "FuelPHPで作るWEBアプリケーションのボイラープレート作成"
task :default do
  git_conf = {
    'remote' => "https://git.codebreak.com/naoyes",
    'name' => "naoyes",
    'email' => "naoyes+codebreak@gmail.com",
  }

  apppath = File.join(ENV['path'], ENV['appname'])
  sh "git clone --recursive git://github.com/fuel/fuel.git #{apppath}"
  cd apppath

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
  sh "git config user.name '#{git_conf['name']}'"
  sh "git config user.email '#{git_conf['email']}'"
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

  git_remote = [git_conf['remote'], ENV['appname'] + '.git'].join('/')
  sh "git add ."
  sh "git commit -m 'Initial commit'"
  sh "git remote add origin #{git_remote}"
  sh "git push origin master"
end
