desc "Parse haml layouts"
task :parse_haml do
  print "Parsing Haml layouts..."
  system(%{
    cd _layouts/haml && 
    for f in *.haml; do [ -e $f ] && haml $f ../${f%.haml}.html; done
  })
  puts "done."
end

desc "Launch preview environment"
task :preview do
  Rake::Task["parse_haml"].invoke
  system "jekyll --auto --server"
end

desc "Build site"
task :build do |task, args|
  Rake::Task["parse_haml"].invoke
  system "jekyll"
end

desc "Deploy site"
task :deploy do |task, args|
  dest = ENV["DEST"].dup
  unless dest[dest.size] == ?/
    dest << '/'
  end
  
  system(%{
    rsync -avz --delete _site/* '#{dest}'
  })
end