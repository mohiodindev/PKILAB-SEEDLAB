# PKILAB-SEEDLAB
# instructions PDF
https://seedsecuritylabs.org/Labs_16.04/PDF/Crypto_PKI.pdf

# Task 1: Becoming a Certificate Authority (CA)
Copy the configuration file into current directory:

     cp /usr/lib/ssl/openssl.cnf ./openssl.cnf 
create new sub-directories and files according to what it specifies in its [ CA_default ]section:

      dir = ./demoCA # Where everything is kept
       certs = $dir/certs # Where the issued certs are kept
       crl_dir = $dir/crl # Where the issued crl are kept
       new_certs_dir = $dir/newcerts # default place for new certs.
       database = $dir/index.txt # database index file.
       serial = $dir/serial # The current serial number
       mkdir PKI
       cp "/usr/lib/ssl/openssl.cnf" "/home/seed/PKI/"
       mkdir demoWK
       cd demoWK
       mkdir certs crl newcerts
       echo 1000 > serial
       gedit index.txt
       https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/91c23f19cf6cfe5b205d0789d6d320b3585d1c14/task_1%20pki.png





 
