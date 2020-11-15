Everything borrowed from: https://guides.rubyonrails.org/getting_started.html

Things to install:

<ul>
<li>Ruby</li>
<li>SQLite3</li>
<li>Node.js</li>
<li>Yarn</li>
</ul>

Run this code to install rails:
<code>gem install rails</code>.

Rails structure summary:

<table>
<tbody>
<tr>
<td>app/</td>
<td>Contains the controllers, models, views, helpers, mailers, channels, jobs, and assets for your application. You'll focus on this folder for the remainder of this guide.</td>
</tr>
<tr>
<td>bin/</td>
<td>Contains the rails script that starts your app and can contain other scripts you use to setup, update, deploy, or run your application.</td>
</tr>
<tr>
<td>config/</td>
<td>Configure your application's routes, database, and more. This is covered in more detail in <a href="configuring.html">Configuring Rails Applications</a>.</td>
</tr>
<tr>
<td>config.ru</td>
<td>Rack configuration for Rack based servers used to start the application. For more information about Rack, see the <a href="https://rack.github.io/">Rack website</a>.</td>
</tr>
<tr>
<td>db/</td>
<td>Contains your current database schema, as well as the database migrations.</td>
</tr>
<tr>
<td>Gemfile<br>Gemfile.lock</td>
<td>These files allow you to specify what gem dependencies are needed for your Rails application. These files are used by the Bundler gem. For more information about Bundler, see the <a href="https://bundler.io">Bundler website</a>.</td>
</tr>
<tr>
<td>lib/</td>
<td>Extended modules for your application.</td>
</tr>
<tr>
<td>log/</td>
<td>Application log files.</td>
</tr>
<tr>
<td>package.json</td>
<td>This file allows you to specify what npm dependencies are needed for your Rails application. This file is used by Yarn. For more information about Yarn, see the <a href="https://yarnpkg.com/lang/en/">Yarn website</a>.</td>
</tr>
<tr>
<td>public/</td>
<td>The only folder seen by the world as-is. Contains static files and compiled assets.</td>
</tr>
<tr>
<td>Rakefile</td>
<td>This file locates and loads tasks that can be run from the command line. The task definitions are defined throughout the components of Rails. Rather than changing <code>Rakefile</code>, you should add your own tasks by adding files to the <code>lib/tasks</code> directory of your application.</td>
</tr>
<tr>
<td>README.md</td>
<td>This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on.</td>
</tr>
<tr>
<td>storage/</td>
<td>Active Storage files for Disk Service. This is covered in <a href="active_storage_overview.html">Active Storage Overview</a>.</td>
</tr>
<tr>
<td>test/</td>
<td>Unit tests, fixtures, and other test apparatus. These are covered in <a href="testing.html">Testing Rails Applications</a>.</td>
</tr>
<tr>
<td>tmp/</td>
<td>Temporary files (like cache and pid files).</td>
</tr>
<tr>
<td>vendor/</td>
<td>A place for all third-party code. In a typical Rails application this includes vendored gems.</td>
</tr>
<tr>
<td>.gitignore</td>
<td>This file tells git which files (or patterns) it should ignore. See <a href="https://help.github.com/articles/ignoring-files">GitHub - Ignoring files</a> for more info about ignoring files.</td>
</tr>
<tr>
<td>.ruby-version</td>
<td>This file contains the default Ruby version.</td>
</tr>
</tbody>
  </table>
  
  To run server:
  <nano>rails server</nano>
  
  Here's where it's running: [http://localhost:3000]
  
  How rails is operating:
  A controller's purpose is to receive specific requests for the application. Routing decides which controller receives which requests. Often, there is more than
  one route to each controller, and different routes can be served by different actions. Each action's purpose is to collect information to provide it to a view.
  
  A view's purpose is to display this information in a human readable format. An important distinction to make is that it is the controller, not the view, where information is collected. The view should just display that information. By default, view templates are written in a language called eRuby (Embedded Ruby) which is processed by the request cycle in Rails before being sent to the user.
  
  We will need to create a new resources. A resource is the term used for a collection of similar objects, such as articles, people, or animals. You can create,
  read, update, and destroy items for a resource and these operations are referred to as CRUD operations.

Rails provides a resources method which can be used to declare a standard REST resource. We need to add the resource to the config/routes.rb so the file will look as follows:

<nano>Rails.application.routes.draw do
  get 'path'
 
  resources : resourceName
 
  root 'path'
end </nano>

Running <nano>rails routes </nano> shows you the setup for the resource. 

We then create a controller for each resource using <nano> rails generate controller resourceName</nano>

In the controller.rb file we write the actions of the controller like this:

<nano>
class ArticlesController < ApplicationController
  def new
  end
end</nano>
  
  In your view file there should be something like this: new.html.erb. 
  
  The extension of this file name is important: 
  
  the first extension is the format of the template, and the second extension is the handler that will be used to render the template. Rails is attempting to find a template called articles/new within app/views for the application. The format for this template can only be html and the default handler for HTML is erb. Rails uses other handlers for other formats. builder handler is used to build XML templates and coffee handler uses CoffeeScript to build JavaScript templates. Since you want to create a new HTML form, you will be using the ERB language which is designed to embed Ruby in HTML.
  
 

Controller Spec:

<nano>
def create
  render plain: params[:resourceName].inspect
end
</nano>

The render method here is taking a very simple hash with a key of :plain and value of params[:article].inspect. The params method is the object which represents the parameters (or fields) coming in from the form. The params method returns an ActionController::Parameters object, which allows you to access the keys of the hash using either strings or symbols. In this situation, the only parameters that matter are the ones from the form.

<nano> def show
  @article = Article.find(params[:id])
  end
 
  def new
  end</nano>
  
  
Models are generated using this following code on terminal
<nano>Rails generate model Resource title:string text:text</nano>


  
