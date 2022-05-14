# Nirvasa API

### Versions

- Ruby 3.0.2
- Rails 6.1.4.1

## Local running 

### 0. Prerequisites

The setups steps expect following tools installed on the system (we recommend using Linux / Mac OS):

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Ruby 3.0.2](https://ryanbigg.com/2014/10/ubuntu-ruby-ruby-install-chruby-and-you)
- [Rails 6.1.4](https://ryanbigg.com/2014/10/ubuntu-ruby-ruby-install-chruby-and-you)
- [PostgreSQL](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-20-04)
- Geos: ```apt-get install libgeos-dev```

### 1. Clone the repository

```bash
git clone https://github.com/LinkUpStudioOld/nirvasa_back.git
```
### 2. Install all dependencies

Install the gems specified in Gemfile:

```bash
bundle install
```

### 3. Create config/local_env.yml with environment variables

Copy the sample .env file and edit it (you can ask other developers about some values).

```bash
cp .env .env.test.local
cp .env .env.development.local
```

### 4. Create and setup the database

Run the following commands to create and setup the database:

```bash
bundle exec rails db:setup
```

### 5. Start the Rails server

You can start the rails server using the command given below.

```bash
bundle exec rails s
```

And now API is available with the following URL: http://localhost:3000.

Admin part here: http://localhost:3000/admin (username: `admin_nirvasa@nirvasa.com`, password: `123456nirvasa`)

To stop the server use `Ctrl` + `C`

### 6. API documentation

Locally you can view documentation with the URL http://localhost:3000/api-docs. 

If there is some error, please execute the following command (it run tests and updates docs):

```bash
bundle exec rake rswag:specs:swaggerize
```

Then restart the server and try again.

### 7. Running the tests

To run the tests just execute the following command:

```bash
bundle exec rspec
```
### 8. Data Import

To download all the data you need to perform initial import. It is performed with the following command in console:

```bash
InsertWorker.perform_async([*list of boards needed*])
```

For example if you need data only from TREB you should write:

```bash
InsertWorker.perform_async(['treb'])
```

Update import is performed every 15 minutes and downloads data for the last 30 minutes. Time period can be modified in the environment variable ```UPDATE_TIME_PERIOD_IN_MINUTES```
# realtor
