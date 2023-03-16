
# Tutorial: Implementing SSL on localhost for Ruby on Rails development with mkcert

In this tutorial, you will learn how to implement an SSL certificate in your Ruby on Rails development environment using mkcert. This can be useful for testing SSL functionality in your application before deploying it to a production server.

## Requirements
- Ruby on Rails 6 or 7 installed on your machine.
- Mkcert installed. You can get it here: https://github.com/FiloSottile/mkcert

## Step 1: Install mkcert

If you haven't installed mkcert yet, follow the instructions in the link mentioned above. Mkcert is a simple command-line tool that generates valid, self-signed SSL certificates for use in local development environments.

## Step 2: Generate SSL certificates

Open your terminal and navigate to the folder where you want to store the certificates. Then, run the following command:

```bash
mkcert localhost
```

This will generate two files: localhost.pem and localhost-key.pem. These files are the certificate and private key, respectively. Make sure these files are stored in a secure and easily accessible location.

## Step 3: Configure Rails to use SSL

Now that we have the certificates, we need to tell Rails to use them. To do this, go to your Rails project folder and edit or create a file called Procfile in the project root (for Rails 6) or edit the existing Procfile.dev file (for Rails 7). Add the following line to the file:

```ruby
web: unset PORT && bin/rails server -b 'ssl://localhost:3000?key=localhost-key.pem&cert=localhost.pem'
```

Make sure the paths to the localhost-key.pem and localhost.pem files are correct. If you stored the files in a different folder, adjust the paths as needed.

## Step 4: Start the Rails server with SSL (only for Rails 6)
If you're using Rails 6, you'll need to install foreman. Open the terminal and navigate to your Rails project folder. Then, run the following command:

```bash
gem install foreman
```

Now that foreman is installed, you can start the Rails server with SSL by running:

```bash
foreman start
```

If you're using Rails 7, foreman is already included by default, and you can simply start the Rails server with SSL by running:

```bash
bin/dev
```

Now your Rails server should be running with SSL enabled. You can access your application by navigating to https://localhost:3000 in your browser.
