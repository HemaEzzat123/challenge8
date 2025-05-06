# Leaky HR Portal  
**Difficulty:** Easy  
**Category:** Web Exploitation  

## Challenge Description  

A hidden HR portal contains sensitive information. Your task is to exploit the data leak and retrieve the flag hidden inside the dashboard.

---

<details>
<summary>Solution</summary>

1. **Index Page Analysis**:  
   - Upon opening `index.html`, the player sees the message:  
     `"Check our internal portal for more info."`  
   - A hidden hint is found in the page's source code:  
     ```html
     <!-- Try exploring: careers.internal.hexacore.htb -->
     ```  
     *(This hint points to a hidden subdomain.)*

2. **Accessing the Subdomain**:  
   - Add `careers.internal.hexacore.htb` to `/etc/hosts`.  
   - Visit:  
     `https://careers.internal.hexacore.htb`

3. **Reconnaissance**:  
   - Check `robots.txt`:  
     Visiting `https://careers.internal.hexacore.htb/robots.txt` reveals:  
     ```
     User-agent: *
     Disallow: /data/
     ```  
     *(This indicates a hidden `/data` directory.)*

4. **Exploiting the Data Leak**:  
   - Access the hidden directory:  
     `https://careers.internal.hexacore.htb/data/employees.json`  
   - The JSON file contains credentials:  
     ```json
     {
       "email": "aya.ayman@hexacore.htb",
       "password": "Winter2024!"
     }
     ```

5. **Authentication**:  
   - Use the credentials on the login page:  
     `https://careers.internal.hexacore.htb/login.html`  
   - Successfully redirects to `dashboard.html`.

6. **Flag Retrieval**:  
   - The flag is displayed on `dashboard.html`:  
     **Flag:**  
     `flag{h3x4c0r3_l34ky_hr}`

</details>
