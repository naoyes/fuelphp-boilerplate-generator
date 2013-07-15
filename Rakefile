# encoding: utf-8
desc "FuelPHPで作るWEBアプリケーションのボイラープレート作成"
task :default do
  git_conf = {
    'remote' => "https://git.codebreak.com/naoyes",
    'name' => "naoyes",
    'email' => "naoyes+codebreak@gmail.com",
  }

  remote_name = "myrepo"
  branch = "master"

  git_remote = [git_conf['remote'], ENV['appname'] + '.git'].join('/')

  dir = ENV['path'].split('/')[-1]
  sh "curl get.fuelphp.com/oil | sh"
  cd File.expand_path("..", ENV['path'])

  sh "oil create #{dir}"
  cd "./#{dir}"
  sh "git config user.name '#{git_conf['name']}'"
  sh "git config user.email '#{git_conf['email']}'"
  sh "git checkout -b #{branch}"
  sh "git add ."
  sh "git commit -m 'my first commit.'"

  sh "git remote add #{remote_name} #{git_remote}"
  sh "git push #{remote_name} #{branch}"
end

desc "FuelPHPで作ったWEBアプリケーションのデプロイ"
task :deploy do
  remote_repo = ENV['repo']

  dir = ENV['path'].split('/')[-1]
  cd File.expand_path("..", ENV['path'])
  sh "git clone --recursive #{remote_repo} #{dir}"
  cd dir
  sh "php oil refine install"
  sh "php composer.phar self-update"
  sh "php composer.phar update"
end
