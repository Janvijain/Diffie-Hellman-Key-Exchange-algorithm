# Diffie-Hellman-Key-Exchange-algorithm               
The Diffie–Hellman (DH) Algorithm is a key-exchange protocol that enables two parties communicating over public channel to establish a mutual secret without it being transmitted over the Internet. DH enables the two to use a public key to encrypt and decrypt their conversation or data using symmetric cryptography. Diffie–Hellman key exchange establishes a shared secret between two parties that can be used for secret communication for exchanging data over a public network.                  

This Code calculates the key and sends email from Alice to Bob & Bob to Alice                    
This code successfully sends key in emails                     

Update this emails in the code               
Alice's email = alice_email                    
Bob's_email = bob_email                    

# Source Code
import smtplib                        
import hashlib                          
p = int(input("enter value of p: "))                           
g = int(input("enter value of g: "))                  
a = int(input("enter value of a: "))                      
b = int(input("enter value of b: "))                    
A = (g**a) % p                  
B = (g**b) % p                          
print('g: ',g,' (a shared value), n: ',p, ' (a prime number)')                    
print('\nAlice calculates:')                   
print('a (Alice random): ',a)                        
print('Alice value (A): ',A,' (g^a) mod p')                    
print('\nBob calculates:')                       
print('b (Bob random): ',b)                
print('Bob value (B): ',B,' (g^b) mod p')                  
print('\nAlice calculates:')                     
keyA=(B**a) % p           
print('Key: ',keyA,' (B^a) mod p')                   
#print('Key: ',hashlib.sha256(str(keyA).encode()).hexdigest())                 
s = smtplib.SMTP('smtp.gmail.com', 587)                      
s.starttls()                      
s.login("alice_email", "password")                      
message = hashlib.sha256(str(keyA).encode()).hexdigest()                 
s.sendmail("alice_email", "bob_email", message)                   
s.quit()                   
print('\nBob calculates:')                      
keyB=(A**b) % p                    
print('Key: ',keyB,' (A^b) mod p')                
#print('Key: ',hashlib.sha256(str(keyB).encode()).hexdigest())                 
s = smtplib.SMTP('smtp.gmail.com', 587)                 
s.starttls()                
s.login("bob_email", "password")              
msg = hashlib.sha256(str(keyB).encode()).hexdigest()              
s.sendmail("bob_email", "alice_email", msg)                 
s.quit()                      
