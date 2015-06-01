require "rubygems"
require 'rake'
require 'yaml'
require 'time'

require 'jekyll'

# Define globals

SOURCE = "."

CONFIG = {
    'version' => "0.1",
    'layouts' => File.join(SOURCE, "_layouts"),
    'posts' => File.join(SOURCE, "_posts"),
    'post_ext' => "md"
}

# Usage: rake post title="A Title" [date="2012-02-09"] [tags=[tag1,tag2]] [category="category"]
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
    abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
    title = ENV["title"] || "new-post"
    tags = ENV["tags"] || "[]"
    category = ENV["category"] || ""
    slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

    puts "Title: #{title}"
    puts "Tags: #{tags}"
    puts "Category: #{category}"

    begin
        date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
    rescue => e
        puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
        exit -1
    end
    filename = File.join(CONFIG['posts'], "#{date}-#{slug}.#{CONFIG['post_ext']}")
    if File.exist?(filename)
        abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
    end

    puts "Creating new post: #{filename}"
    puts "#{filename}"
    open(filename, 'w') do |post|
        post.puts "---"
        post.puts "layout: post"
        post.puts "title: \"#{title.gsub(/-/,' ')}\""
        post.puts 'description: ""'
        post.puts "category: #{category}"
        post.puts "tags: #{tags}"
        post.puts "---"
    end
end # task :post

# Usage: rake page name="about.html"
# You can also specify a sub-directory path.
# If you don't specify a file extention we create an index.html at the path specified
desc "Create a new page."
task :page do
    name = ENV["name"] || "new-page.md"
    filename = File.join(SOURCE, "#{name}")
    filename = File.join(filename, "index.html") if File.extname(filename) == ""
    title = File.basename(filename, File.extname(filename)).gsub(/[\W\_]/, " ").gsub(/\b\w/){$&.upcase}
    if File.exist?(filename)
        abort("rake aborted! #{filename} already exists.")
    end

    puts "Creating new page: #{filename}"
    open(filename, 'w') do |post|
        post.puts "---"
        post.puts "layout: page"
        post.puts "title: \"#{title}\""
        post.puts 'description: ""'
        post.puts "---"
    end
end # task :page

desc "Generate blog files"
task :generate do
    Jekyll::Site.new(Jekyll.configuration({
        "source"      => ".",
        "destination" => "_site"
    })).process
end

desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
    Dir.mktmpdir do |tmp|
        cp_r "_site/.", tmp
        Dir.chdir tmp
        system "git init"
        system "git add ."
        message = "Site updated at #{Time.now.utc}"
        system "git commit -m #{message.inspect}"
        # system "git remote add origin git@github.com:xautjzd/xautjzd.github.io.git"
        system "git remote add origin git@github.com:xautjzd/xautjzd.github.io.git"
        system "git push origin master --force"
    end
end
