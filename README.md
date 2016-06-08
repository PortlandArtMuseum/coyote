COYOTE
====

Image annotation site and API to enable the distributed annotation of museum images.

## Usage 

```bash
    #run the server
    bin/rails s

    #automatically run tests as you work
    #you might need to install a shim for guard
    guard

    #run the tests on their own
    bin/rspec

    #run the console
    bin/rails c
```

We could include build status here.

## Setup

```bash
    bundle install

    #set up the .env, override at .env.development and .env.test if needed

    #create the DBs for dev and test
    bin/rake db:create db:migrate db:seed
    RAILS_ENV=test bin/rake db:create db:migrate
```

Secure creds are kept untracked in `.env`

### Vagrant

If you wish to use Vagrant for development, install [vagrant](https://www.vagrantup.com/downloads.html) and run `vagrant up`  Then, you can view the site like so:

```bash

    ssh -N -L 3000:localhost:3000 vagrant@localhost -p 2222 #vagrant is the password
    open http://localhost:3000
```

## Server Install

Spin up a server with a recent Ubuntu server OS.

Install the chef related gems, then the cookbooks.

```bash
cd chef
bundle install
librarian-chef install
```

Edit the `.env` to accound for your particulars.

Generate an SSL if you need to and add to your data bag.

Build the server and execute the recipes

```bash
knife solo prepare root@myserver.com
knife solo prepare root@myserver.com
```





## Components

- [RubyOnRails](http://rubyonrails.org/)
- [accecess](http://lukyvj.github.io/accecss/)
- [MariaDB](https://mariadb.org/) 
- [rbenv](http://rbenv.org/) with [plugins](https://github.com/sstephenson/rbenv/wiki/Plugins) for gems, bundler, build, and binstubs
- [bundler](http://bundler.io/).
- [SASS](http://sass-lang.com/)
- [Coffeescript](http://coffeescript.org/)

## Data model

For use on [nomnoml](http://www.nomnoml.com/)

    [<frame>Coyote data model|
      [User | id: int | first_name: string | last_name: string |  email: string | admin: bool | timestamps]
      [Image | id: int |url : string | canonical_id: string]
      [Tag | id: int | title: string]
      [Group | id: int | title: string]
      [Description | id: int | locale:str(en) | text: text | timestamps]
      [Website | id: int | url: string | title: string | timestamps]
      [Status | id: int | title: string | description: text]
      [Meta| id: int| title: string | instructions: text]

      [Website]->[Group]

      [Image]->[Group]

      [Assignment]->[Image]
      [Assignment]->[User]

      [Description]->[User]
      [Description]->[Meta]
      [Description]->[Status]

      [Image] +-> 0..* [Description]
      [Image] +-> 0..* [Tag]
    ]

 
## Links

- [MCA Coyote Repo](https://github.com/mcachicago/coyote)
- [Museum of Contemporary Art Chicago](http://www2.mcachicago.org/) 
- [A11Y Guidelines](http://a11yproject.com/)
- [Sina's Links on Accessibility](http://www.sinabahram.com/resources.php)
- [ARIA in HTML](http://rawgit.com/w3c/aria-in-html/master/index.html) and [ARIA](http://www.w3.org/TR/wai-aria/states_and_properties#global_states)

## Versus
- [Depict4](http://depictfor.us/)
- [Autotune](https://github.com/voxmedia/autotune/)
