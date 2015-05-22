# docker-httpd

This is a docker component that leverages a minimalistic, but working
HTTPd in Tcl.  The HTTPd implementation comes from the
[til](https://github.com/efrecon/til).  Being based on a [micro-sized
Tcl core image](https://github.com/efrecon/mini-tcl), this results in
an image just above 20MB.

The component has the following features:

* It serves on the HTTP alternative port, i.e. `8080`.  Run the
  component with `-p 8080:8080` or the host port of your choice.

* It exports a volume at `/opt/www` which is the root of the
  directories that it serves.  Arrange to mount to that directory a
  local directory using an option like `-v /var/mywww:/opt/www:ro`.
  Using the `ro` is probably a good idea to increase security if you
  just want to serve files.

* You can access logging through mounting the volume `/opt/log` if
  necessary.

This component is only meant to server files on HTTP, not even HTTPS.
It allows directory listing.  The underlying web server module is
actually much more capable than that: it supports HTTPS,
authentication, websockets, REST, etc.  But none of these features
surfaces here to keep the component to a bare minimum when it comes to
features and functionality.
