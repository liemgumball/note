Created: July 26, 2024 10:12 AM
Class: Self-Research
Type: Code
Materials: https://medium.com/@devkosal/switching-java-jdk-versions-on-macos-80bc868e686a#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6ImYyZTExOTg2MjgyZGU5M2YyN2IyNjRmZDJhNGRlMTkyOTkzZGNiOGMiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxMDg5ODcyMzA0ODczMTIzOTQ2NTMiLCJlbWFpbCI6ImxpZW0xNzYyMDAxQGdtYWlsLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJuYmYiOjE3MjE5NjIwODEsIm5hbWUiOiJUaGFuaCBMacOqbSBOZ3V54buFbiIsInBpY3R1cmUiOiJodHRwczovL2xoMy5nb29nbGV1c2VyY29udGVudC5jb20vYS9BQ2c4b2NJMXdpTGl0WHRuVmlaSzM4aVhzQWRSZEY2WHZfUHBDQWtWSHE0a2k0Umxfa2JNbHJtdT1zOTYtYyIsImdpdmVuX25hbWUiOiJUaGFuaCBMacOqbSIsImZhbWlseV9uYW1lIjoiTmd1eeG7hW4iLCJpYXQiOjE3MjE5NjIzODEsImV4cCI6MTcyMTk2NTk4MSwianRpIjoiNTVkYjhiZjc3NGMwYTc4MGY4MmZmNzU0M2E1N2QxMDAwNGQ5NmU0NyJ9.pVQEfgpzkOXV6YjHl3zq4GFF9pobC70CnDfI-u_mteD9WzGn80EepyR5tvD531jnJBoorLoGByda_Mtmf604GzkyA6PLKkhRrStyjaZ8su68hoEhlZh0JVXJxekKexQ70AKIeiilHDTtrAQOD3uVmdyyk5DoTwgvfP-Df1qzXAMTNWXPefDZYG1rZCu34_uxqJTLNUUiVka55RHXGPi3rONMZ1OPA0h2q3_iXtcq-a3FIDkfxvCUSKqv1EcU2uh-j6U5wNyVgZUcB-LNXxq1r7kl3d0isf1AIFnjIGxZ9CVFhEdURm9dI6D00W3IslPq_22w0wf8nwTVREMm2SJTJw
Reviewed: No
Edited: July 26, 2024 10:33 AM

# 1. List all JDK versions

```bash
# macOS
/user/libexec/java_home -V

# Matching Java Virtual Machines (2):
#    21.0.4 (arm64) "Oracle Corporation" - "Java SE 21.0.4" /Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home
#    17.0.12 (arm64) "Oracle Corporation" - "Java SE 17.0.12" /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home

```

# 2. Check current JDK used

```bash
java --version
# java 17.0.12 2024-07-16 LTS
# Java(TM) SE Runtime Environment (build 17.0.12+8-LTS-286)
# Java HotSpot(TM) 64-Bit Server VM (build 17.0.12+8-LTS-286, mixed mode, sharing)
```

# 3. Switch version by export env variable

```bash
export JAVA_HOME=`/usr/libexec/java_home -v 17`
```

# 4. Check version

```bash
java --version
# java 21.0.4 2024-07-16 LTS
# Java(TM) SE Runtime Environment (build 21.0.4+8-LTS-274)
# Java HotSpot(TM) 64-Bit Server VM (build 21.0.4+8-LTS-274, mixed mode, sharing)
```