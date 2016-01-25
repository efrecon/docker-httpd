# docker-httpd

This is a docker component that leverages a minimalistic, but working HTTPd in
Tcl. The HTTPd implementation comes from the [til](https://github.com/efrecon/til).
Being based on a [micro-sized Tcl core image](https://github.com/efrecon/mini-tcl),
this results in an image just above 20MB.

The component has the following features:

* It serves on the HTTP alternative port, i.e. `8080`. Run the component with
  `-p 8080:8080` or the host port of your choice.

* It exports a volume at `/opt/www` which is the root of the directories that it
  serves. Arrange to mount to that directory a local directory using an option
  like `-v /var/mywww:/opt/www:ro`. Using the `ro` is probably a good idea to
  increase security if you just want to serve files.

* You can access logging through mounting the volume `/opt/log` if
  necessary.
  
* You can provide it with a pair of public and private key with the -pki option
  to make it serve requests on HTTPS instead of plain HTTP. The current
  implementation serves as many protocols as possible.
  
* You can make it protect some or all directories that it serves using the
  -authorization option. This is a list which is a multiple of three, its
  elements being, respectively: a glob-style pattern matching the paths to
  protect, a Realm, a list of user:password specification (with the separating
  colon). The list can be sourced from a file instead, specify a `@` followed by
  the path to the file as the value for the option. You can use the `/opt/data`
  exported volume to mount that file from your local host.

This component is only meant to server files on HTTP. It allows directory
listing. The underlying web server module is actually much more capable than
that: websockets, REST, etc. But none of these features surfaces here to keep
the component to a bare minimum when it comes to features and functionality.
