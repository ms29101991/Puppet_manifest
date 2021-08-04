# Puppet_manifest
# Install the Apache HTTP Server:
 package{'package':
   name   =>  'httpd'
   ensure => 'installed',
  }
  
  # Edit the main Apache configuration file to adjust the resource use settings.
  
  $myservice_content =  
            StartServers        4
            MinSpareServers     20
            MaxSpareServers     40
            MaxClients          200
            MaxRequestsPerChild 4500
        </IfModule>
		
  file{'/etc/httpd/conf/httpd.conf':
    ensure  => present,
    content => $myservice_content,
  }
 
 
 # Configure Apache for Virtual Hosting
 
  $myapache_content = info = <VirtualHost *:80>
             ServerAdmin admin@example.org
             ServerName example.org
             ServerAlias www.example.org
             DocumentRoot /srv/www/example.org/public_html/
             ErrorLog /srv/www/example.org/logs/error.log
             CustomLog /srv/www/example.org/logs/access.log combined
        </VirtualHost>
		
	 file{ '/etc/httpd/conf.d/vhost.conf':
    ensure  => present,
    content => $myapache_content,
  }	
  
  
  # Create the directories referenced above:
  
  file { ' /srv/www/example.org/public_html':
    ensure => 'directory',
  }
  
  file { ' /srv/www/example.org/logs':
    ensure => 'directory',
  }
  
  # Start Apache:
  
  service { 'httpd':
     ensure => 'restart',
	 enable => 'true'
  }
  
  package {' mod package':
  name     => 'mod_perl',
  ensure => installed,
}
