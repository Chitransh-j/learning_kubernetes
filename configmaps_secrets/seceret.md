Secrets and configMaps are very similar in implementation but secrets are generally 
preferred to store the namesake. Out of the box they aren't encrypted and it is our responsiblity to encrypt them. Anybody with an access to kubectl(API server basically of the control Plane) has access to the secrest if kept unencrypted. 


