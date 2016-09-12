Angular Webserver Guide


## Install Ruby
1. Install [Homebrew](http://brew.sh/) (Mac Only):
    ```
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    ```

2. Install (or upgrade) Ruby:
    ```
    brew install ruby
    ```



### Use Ruby Gems to install Bundler & Rack
1. Install Bundler

    ```
    sudo gem install bundler
    ```


2. Create a `Gemfile` inside your project and put:

    ```
    source 'https://rubygems.org'
    gem 'rack'
    ```

3. Run & Install

    ```
    bundle install
    ```


### Setup Rack for webserver emulation:

1. Create a file called `config.ru` on the same level as your `src` folder. Which is what contians your static files (`js`, `css`, and `images` directory) as well as your `index.html` file. Inside the `config.ru` file, add:
    ```
    use Rack::Static,
      :urls => ["/images", "/js", "/css", "/templates"],
      :root => "src"

    run lambda { |env|
      [
        200,
        {
          'Content-Type'  => 'text/html',
          'Cache-Control' => 'public, max-age=86400'
        },
        File.open('src/index.html', File::RDONLY)
      ]
    }

    ```

2. Run `rackup` in Terminal/Command Prompt.



