# GPUMAGIC
A C++ Nix AMD Graphics Card Control Server And Client

Author: DominiLux
License: Undecided - Please feel free to suggest a license type prior to me releasing the code.  I know I don't want to use a GPL.  I am leaning for either BSD, APACHE 2.0, OR MIT.  I'll have to study the more to see which is more popular amongst orginizations needing this software.

# Features
Below is a list of features for each portion of the project.  The portions are broken down into the Daemon, Server, and Client
## Daemon
- Runs with a low memory footprint directly on the node and establishes a basic command line interface.
- The Daemon itself runs as root thus allowing non-root users to utilize it.  For security, non root users must be added to the GPUMAGIC group before the daemon will accept any commands from them.  This allows system administrators to easily set up specific accounts that have access to the daemon while still maintaining a secure environment. (Plays well with LDAP deployments for large scale computational clusters)
- Direct over clocking and under clocking of the GPU
- Direct over clocking and under clocking of the VRAM
- Under volting and over volting the GPU
- Under volting and over volting the memory controler
- VBIOS Dump
- VBIOS Flash
- Get Temperatures
- List Available Devices
- Set GPU Fans
- Auto adjust gpu fan speeds based on a target temperature... (When more than one GPU is present it is intellegent enough to figure out the position of various GPU's in a computational node and dynamically adjust GPU temperatures throughout the unit until the GPU most affected by heat build up from other GPU's has reached it's target.  Essentially the algorythm takes into account that it is more energy effecient to cool a GPU on the outside of a stack lower than the target verses running the fans in the middle of the stack at 100%.  This should lead to an overall increase in performance and longevity in your GPU investments).
## JSon RPC Server
- Runs as a normal user within the GPUMAGIC group thereby only allowing it to perform GPU related tasks (For hardened security)
- Utilizes secure OpenSSL private/shared key signing pairs for a secure private tunnel to controller clients
- Can be configured to also authenticate against an LDAP server for added security
- Acts as a wrapper to the command line Daemon via a port open within the lan (The encryption and tuneling ensure enterprise grade security for this use and the limited access the server has on the system acts as a second line of defense in case of some sort of Zero Day attack)
- Will issue commands to the Daemon from remote users so long as the client they are running has the appropriate private/shared keys and, they were able to be authenticated against the LDAP server(If configured for LDAP security)
- Lan Broadcast / Autodiscover allows for clients within a LAN to auto map servers for monitoring.  During the negotiation process the client will determine if it has access to monitor/control a given server or not.
## Client
 - Designed for remote administration of a lan or for central datacenter control room administration depending on how it is configured.
 - Communicates with the JSon RPC Server
 - Fully integrated with server security features
 - Will work over a virtual private network for remote maintenance
 - Utilizes SQL or NoSQL backend database for gpu monitoring data to be stored (Allows for an easy front end user interface to be custom created in php or another simple language, also helps with diagnostics and troubleshooting to have historical data on all GPU's within a node and all nodes within a cluster).
 - Enterprise grade solution
# Installation
Currently being tested and debugged.  Also I am writing all nesscerry documentation for it.  Once this phase is done I will upload the completed version of the project as the master branch and split off a development branch for adding new features and other experiminitation.  Please feel free to leave comments or feature requests while I work towards a publishable version. 
