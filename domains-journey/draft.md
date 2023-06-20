
# About Domains

### DNS

A **Domain** refers to a distinct address used to identify a website. Instead of using an application's IP addresses to access the application, you can type a domain into a web browser, such as `example.com`. 

When you type a domain name into a browser or access a link, your computer initiates a Domain Name System (DNS) query to translate that domain name into the IP address of the application. This process, called **DNS resolution**, involves multiple steps.

(image: DNS resolution, servers and client)

First, it checks local cache to see if it has resolved the domain name before. If not, it sends the query to your internet service provider's (ISP) *DNS resolver*.

The resolver then communicates with multiple DNS servers until it receives the IP address associated with the domain. Finally, the resolver returns the IP address to your computer and the browser interprets the page.

### Elements of a domain

A domain is made up of several components that identify applications on the internet. These elements of domains that are registered in DNS servers can be referred to as a fully qualified domain name (FDQN), which looks something like this:

(image: FDQN of blog.example.com)
DNS resolution begins from right to left, which means the first and highest component in the hierarchy of a domain is the **top-level domain** (TLD). Common TLDs include `.com`, `.org`, and `.net`. TLDs are responsible for managing DNS registries and maintaining the nameservers for the domains registered under them.

After DNS resolves the TLD, it proceedes to the **domain** itself, in this case, the word `example`. Domains are identifiers used to represent websites on the internet and can be registered and owned by individuals or organizations.

If a **subdomain** is registered, the resolution finally skips to this last element, which in this case, is represented by the word `blog`. Subdomains are extensions of a domain and can be further divided into additional levels. Each subdomain can have its own DNS records, allowing for separate configuration and management within the larger domain.

### Domain providers

- how to acquire domain (costs, maintenance)
- register new records (add subdomain)
- other types of records (email)
- records table?

