
bundle exec jekyll build
bundle exec jekyll serve

cp -R _site/* /Users/jamesdhope/Documents/Personal/_site/jamesdhope.github.io/
cd _site
git add .
git commit -m ""
git push 

