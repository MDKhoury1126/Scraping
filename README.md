```import urllib.request
# open URL like a browser, send an HTTP request, receive the HTML back, read bytes from server.
import urllib.error
# defines error types for urllib.request
import ssl
# module for handling SSL certificates, allows us to ignore SSL certification errors
from bs4 import BeautifulSoup
# BeautifulSoup is a library for parsing HTML and XML documents, it creates a parse tree for parsed pages that can be used to extract data from HTML, which is useful for web scraping.

# Ignore SSL certificate errors
ctx = ssl.create_default_context()
# loads Python's default SSL settings, which include verifying SSL certificates. By creating a default context, we can modify its settings to ignore SSL certificate errors.
ctx.check_hostname = False
# This line disables hostname checking in the SSL context. Hostname checking is a security feature that ensures the hostname in the URL matches the hostname in the SSL certificate. By setting this to False, we are telling Python to ignore this check, which can be useful when dealing with self-signed certificates or when we don't care about the authenticity of the server.
ctx.verify_mode = ssl.CERT_NONE
# This line sets the verification mode of the SSL context to CERT_NONE, which means that the SSL context will not verify the server's SSL certificate at all. This is generally not recommended for production code, as it can expose you to security risks, but it can be useful for testing or when dealing with servers that have self-signed certificates.

url = input('Enter URL: ')
# This line prompts the user to enter a URL and stores the input in the variable 'url'. This URL will be used later to fetch the HTML content of the page.

HTML = urllib.request.urlopen(url, context=ctx).read()
# This line opens the URL specified by the user, using the SSL context we created earlier to ignore SSL certificate errors. It sends an HTTP request to the server and reads the response, which is the HTML content of the page. The resulting HTML is stored in the variable 'HTML' as a byte string.
soup = BeautifulSoup(HTML, "html.parser")
# HTML is what we need parsed and 'html.parser' is the parser we want to use. BeautifulSoup will take the HTML content and create a parse tree that we can navigate to extract data from the HTML.
tags = soup('span')
# shortcut for soup.find_all('span'), which finds all the <span> tags in the HTML document and returns them as a list. The resulting list of <span> tags is stored in the variable 'tags'.
# need to find the numbers in the span tags
total = 0

for tag in tags:
    num = int(tag.text)
    total += num

print(total)```
