# docker-stack
This is my docker stack for development
It contains the following components:
* Traefik Router/LoadBalancer
* MailDev SMTP Server for local mail testing
* Backend
  * PHP-FPM (latest) with Symfony CLI installed
  * Nginx (latest) as Webserver for PHP Application
  * ASP.NET Core (3.0) Sample Application
* SQL
  * Maria DB (latest)
  * MS SQL Server (latest)

Feel free to use whole environment or pick some parts.
I've composed everything by researching other repos and using my own knowledge.
But I need to say that I'm not a docker specialist and this is my first try that works.
The focus was on minimalistic images that fulfill my needs.  
