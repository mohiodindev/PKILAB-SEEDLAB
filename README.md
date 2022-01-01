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
          -out	Specifies the output file where the result will be stored.
            -config	Configuration file to be specified. 

create new sub-directories and files 
     
       mkdir PKI
       cp "/usr/lib/ssl/openssl.cnf" "/home/seed/PKI/"
       mkdir demoWK
       cd demoWK
       mkdir certs crl newcerts
       echo 1000 > serial
       gedit index.txt
  https://github.com/ghulammohiodin/PKILAB-SEEDLAB/blob/91c23f19cf6cfe5b205d0789d6d320b3585d1c14/task_1%20pki.png

Start to generate the self-signed certificate for the CA:

return to the parent directory

     cd ..
    openssl req -new -x509 -keyout ca.key -out ca.crt -config openssl.cnf 




 
