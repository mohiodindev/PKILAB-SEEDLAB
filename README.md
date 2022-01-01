# PKILAB-SEEDLAB
# instructions PDF
https://seedsecuritylabs.org/Labs_16.04/PDF/Crypto_PKI.pdf

# Task 1: Becoming a Certificate Authority (CA)
Copy the configuration file into current directory:

     cp /usr/lib/ssl/openssl.cnf ./openssl.cnf 
   what does this comand means
     
         req	Creates a signing request.
        -new	Creates new requests.
       -x509	Inspects signed certificate by loading x509 modules.
       -keyout	Used to give a path to a filename, where it writes newly created private keys. 
       -out	Specifies the output file where the result will be stored
       -config	Configuration file to be specified. 

create new sub-directories and files 
     
       mkdir PKI
       cp "/usr/lib/ssl/openssl.cnf" "/home/seed/PKI/"
       mkdir demoWK
       cd demoWK
       mkdir certs crl newcerts
       touch 1000 > serial
       gedit index.txt
  ATTACHED SCREENSHOTS
  https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/91c23f19cf6cfe5b205d0789d6d320b3585d1c14/task_1%20pki.png
  https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/75734d4870c3b01215b64dd5051e1629a1584456/task_1_1pki.png

Start to generate the self-signed certificate for the CA:

return to the parent directory

     cd ..
    openssl req -new -x509 -keyout ca.key -out ca.crt -config openssl.cnf 
    
      
      Generating a 2048 bit RSA private key
      ...................+++
         .............................................................................+++
      writing new private key to 'ca.key'
     Enter PEM pass phrase:
     Verifying - Enter PEM pass phrase:
     -----
    You are about to be asked to enter information that will be incorporated
    into your certificate request.
    What you are about to enter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', the field will be left blank.
    -----
    Country Name (2 letter code) [AU]:pk
     State or Province Name (full name) [Some-State]:Panjab
    Locality Name (eg, city) []:swl
    Organization Name (eg, company) [Internet Widgits Pty Ltd]:uosahiwal
    Organizational Unit Name (eg, section) []:uosahiwalbscs
     Common Name (e.g. server FQDN or YOUR name) []:mohiodin
      Email Address []:mohiodin@test.com
 
 
 # Task 2: Creating a Certificate for SEEDPKILab2021.com
   ATTACHED SCREENSHOTS 
   https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/721eca5780ea0a0826d49873b2af8aee569b9a53/task_2.png
   https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/721eca5780ea0a0826d49873b2af8aee569b9a53/task_2_2.png
   https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/721eca5780ea0a0826d49873b2af8aee569b9a53/task_2_3.png
https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/63c105dc066ec4f633618199f67f16ee59754a7c/task_2_4.png
# Step 1: Generate public/private key pair.

       
       openssl genrsa -aes128 -out server.key 1024
 The server.key is an encoded text file (also encrypted), so you will not be able to see the actualcontent, such as the modulus, private exponents, etc. To see those, you can run the following command:
 
      openssl rsa -in server.key -tex
      
# Step 2: Generate a Certificate Signing Request (CSR)
       openssl req -new -key server.key -out server.csr -config openssl.cnf
# Step 3: Generating Certificates
     openssl ca -in server.csr -out server.crt -cert ca.crt -keyfile ca.key \
    -config openssl.cnf
If OpenSSL refuses to generate certificates, it is very likely that the names in your requests do not match
with those of CA. The matching rules are specified in the configuration file (look at the [policy match]
section). You can change the names of your requests to comply with the policy, or you can change the policy.
The configuration file also includes another policy (called policy anything), which is less restrictive.
You can choose that policy by changing the following line:


       "policy = policy_match" change to "policy = policy_anything".

# Task 3: Deploying Certificate in an HTTPS Web Server

ATTACHED SCEENSHOTS
https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/a15b9b96776cbc9732e17b203890f5bd7f7c96cc/task_5_1.png
https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/a15b9b96776cbc9732e17b203890f5bd7f7c96cc/task%23_3.png
https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/a15b9b96776cbc9732e17b203890f5bd7f7c96cc/task_3_1.png
https://github.com/ghulammohiodin/PKILAB-
SEEDLAB/blob/a15b9b96776cbc9732e17b203890f5bd7f7c96cc/task_3_2.png
https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/a15b9b96776cbc9732e17b203890f5bd7f7c96cc/tsk_3.png
 
 
# Step 1: Configuring DNS.

   edit 
   
   
     /etc/hosts/
  and add this 
        
        
        127.0.0.1 SEEDPKILab2021.com

# Configuring the web server.
 Combine the secret key and certificate into one file
 
        cp server.key server.pem
        cat server.crt >> server.pem
# Launch the web server using server.pem
     openssl s_server -cert server.pem -www
Goto browser and write 


        https://SEEDPKILab2021.com
# Getting the browser to accept our CA certificate
    Edit -> Preference -> Privacy & Security -> View Certificates.
    
#  Testing our HTTPS website
. Modify a single byte of server.pem, and restart the server, and reload the URL. What do you
observe? Make sure you restore the original server.pem afterward. Note: the server may not be
able to restart if certain places of server.pem is corrupted; in that case, choose another place to
modify.
2. Since SEEDPKILab2021.com points to the localhost, if we use https://localhost:4433
instead, we will be connecting to the same web server. Please do so, describe and explain your
observations


#  Task 4: Deploying Certificate in an Apache-Based HTTPS Website
  ATTACHED SCREENSHOTS
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/a15b9b96776cbc9732e17b203890f5bd7f7c96cc/task_4.png
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/cbfdcd429203781907fa40c2ca7310cd3365190b/task_4_3.png
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/cbfdcd429203781907fa40c2ca7310cd3365190b/task_4_4.png
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/cbfdcd429203781907fa40c2ca7310cd3365190b/task_4_5.png
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/cbfdcd429203781907fa40c2ca7310cd3365190b/task_4_6.png
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/cbfdcd429203781907fa40c2ca7310cd3365190b/task_4_7.png
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/cbfdcd429203781907fa40c2ca7310cd3365190b/task_4_8.png
         
 Make a directory in  
 
           
           
         /var/www/
 and copy 
 
         
         
        index.html                    
 in it 
 
        cd /var/www/
        sudo mkdir seedpki
        sudo cp "/var/www/html/index.html/" "/var/www/seedpki/"
To add an HTTPS website, we need to add a VirtualHost entry to the default-ssl.conf file
in the same folder.



     <VirtualHost *:443>
     ServerName two.example.com
    DocumentRoot /var/www/Example_Two
    DirectoryIndex index.html
      SSLEngine On
     SSLCertificateFile /etc/apache2/ssl/example_cert.pem ➀
    SSLCertificateKeyFile /etc/apache2/ssl/example_key.pem ➁
    </VirtualHost>        
  
After the default-ssl.conf file is modified, we need to run a series of commands to enable SSL.
Apache will ask us to type the password used for encrypting the private key. Once everything is set up
properly, we can browse the web site, and all the traffic between the browser and the server will be encrypted

     Test the Apache configuration file for errors
     sudo apachectl configtest
    // Enable the SSL module
      sudo a2enmod ssl
    // Enable the site we have just edited
     sudo a2ensite default-ssl
    // Restart Apache
    sudo service apache2 restart
    


    
 
        





 



 
