## Queuing System in JS

### Securing Redis
By default Redis binds to all the interfaces and has no authentication at all. If you use Redis in a very controlled environment, separated from the external internet and in general from attackers, that's fine. However if an unhardened Redis is exposed to the internet, it is a big security concern. If you are not 100% sure your environment is secured properly, please check the following steps in order to make Redis more secure, which are enlisted in order of increased security.

- Make sure the port Redis uses to listen for connections (by default 6379 and additionally 16379 if you run Redis in cluster mode, plus 26379 for Sentinel) is firewalled, so that it is not possible to contact Redis from the outside world.
- Use a configuration file where the bind directive is set in order to guarantee that Redis listens on only the network interfaces you are using. For example only the loopback interface (127.0.0.1) if you are accessing Redis just locally from the same computer, and so forth.
- Use the requirepass option in order to add an additional layer of security so that clients will require to authenticate using the AUTH command.
- Use spiped or another SSL tunneling software in order to encrypt traffic between Redis servers and Redis clients if your environment requires encryption.

Note that a Redis instance exposed to the internet without any security is very simple to exploit, so make sure you understand the above and apply at least a firewall layer. After the firewall is in place, try to connect with redis-cli from an external host in order to prove yourself the instance is actually not reachable.
