require 'pry'
require 'yaml'
require 'erb'
require 'pty'

desc "start postgresql server"
task :start do
  start!
end

desc "stop postgresql server"
task :stop do
  stop!
end

desc "setup postgresql to some version"
task :setup do
  Rake::Task["stop"].invoke if configured?
  if ENV['VERSION'].nil?
    STDERR.puts "usage: rake setup VERSION='<some postgres version from doker hub>'"
    STDERR.puts "   ex: rake setup VERSION=9.5"
  else
    File.open("docker-compose.yml", "w+"){|f| f.puts ERB.new(IO::readlines("docker-compose.yml.erb").join).result }
  end
end

def configured?
  File.exist?("docker-compose.yml")
end

def stop!
  if running_container?
    PTY.spawn("docker-compose down") do |stdout, stdin, pid|
      stdout.each{|line| print line}
    end
  end
rescue Errno::EIO
end

def running_container?
  `docker ps -qa -f status=running | grep "^$(docker-compose ps -q | cut -c1-12)$" | wc -l`.to_i > 0
end

def start!
  if stopped_container?
    PTY.spawn("docker-compose up -d") do |stdout, stdin, pid|
      stdout.each{|line| print line}
    end
  end
rescue Errno::EIO
end

def stopped_container?
  `docker ps -qa -f status=running | grep "^$(docker-compose ps -q | cut -c1-12)$" | wc -l`.to_i == 0
end

task :default, :setup
