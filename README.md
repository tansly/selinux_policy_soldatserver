# selinux_policy_soldatserver

This is an SELinux policy module for the [Soldat](https://soldat.pl/) Dedicated Server.
Surely not many people will be interested in this, but well...

### Types
This module defines the following types:
* **soldatserver\_t**: The domain for the server process.
* **soldatserver\_exec\_t**: The domain for the server executables, entry point for the soldatserver\_t domain.
* **soldatserver\_data\_t**: For all kinds of *read-only* server data, readable by soldatserver\_t.
* **soldatserver\_log\_t**: For log and pid files of the server, writable by soldatserver\_t.
* **soldatserver\_data\_rw\_t**: Read-write data of the server, such as the banned lists, admin lists etc.
* **soldatserver\_port\_t**: For network ports that the server will bind to, such as the game port and the file server port.
* **soldatserver\_lobbyport\_t**: For the port that the server needs to connect to to register itself to the lobby.

Type enforcement rules are derived by using *common sense* and testing.
I will not delve into details here, the module is pretty short and one can
guess the purpose of most lines by using *common sense*.

### File contexts
The module assumes that the server will be placed under `/opt/`.
Under `/opt/`, you can place as many server instances as you like, with the
pattern `/opt/soldatserver_.+`. For example, I run three servers as:
* `/opt/soldatserver_CTF/`
* `/opt/soldatserver_DM/`
* `/opt/soldatserver_RCTF/`

### Notes

* I run the servers as systemd services.
    I did not test any other kind of configuration. However,
    except the pidfile workaround (see the .te file) that I'm not sure if
    necessary, there should be no stuff dependant on systemd or
    any other stuff in my distro (Fedora Workstation 28). Still,
    [here is my systemd unit template.](https://gist.github.com/0c2edf043334f11abdddc5d7613c59a5)

* This module is tested on Fedora Workstation 28, with Soldat Dedicated Server 2.7.1.
    It does not generate any AVC's, and it is the tightest policy I could
    come up with with two days of work. But note that my knowledge of SELinux is
    pretty limited.

