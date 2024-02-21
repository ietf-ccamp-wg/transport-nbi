# Guidelines for multi-layer topology instance

## Network Type

The network-types presence container has been define to support different types of networks as described in section 2.4.4 of \[RFC8345]

~~~~
    +--rw nw:network-types
        +--rw ex:foo-topology!
        +--rw tet:te-topology!
          +--rw ex:bar-topology!
          +--rw ex:baz-topology!
~~~~

A given topology instance may instantiate one or more network type presence containers:

- a single-layer topology instance instantiates the network type for the layer it supports;

- a multi-layer topology instance instantiates multiple network types, one for each layer it supports.

A multi-layer topology instance can also instantiate a mix of TE and non-TE network types:

~~~~
  {
    "ietf-networks:network-types": {
      "example-networks:foo-topology": {},
      "ietf-te-topology:te-topology": {
        "example-networks:bar-topology": {},
        "example-networks:baz-topology": {}
      }
    }
  }
~~~~

## Node Type

A multi-layer topology instance can contains nodes which support one or multiple layers.

In order to report which layer(s) a node can support, it is suggested:

- for non-TE network types, to define a presence container under the node to indicate whether the node supports a given non-TE layer;

- for TE network-types, to define a presence container under the te-node-attributes container to indicate whether the node supports a give TE layer.

~~~~
    +--rw node* [node-id]
       +--rw node-id            node-id
       ....................................................
       +--rw ex:foo-node!
       +--rw tet:te-node-id?   te-types:te-node-id
       +--rw tet:te!
          +--rw te-node-attributes
             +--rw ex:bar-node!
             +--rw ex:baz-node!
~~~~

This approach gives implementation freedom to instantiate or not the te-topology for non-TE network types.

A single layer node has only one node presence container while a multi-layer node has multiple node presence containers, one for each layer it can support.

A multi-layer node can also support a mix of TE and non-TE layers.

## Link Type

A multi-layer topology instance can contains links which support one or multiple layers.

In order to report which layer(s) a link can support, it is suggested:

- for non-TE network types, to define a presence container under the link to indicate whether the node supports a given non-TE layer;

- for TE network-types, to use the interface-switching-capability to list the TE layers the node supports.

~~~~
    +--rw nt:link* [link-id]
       +--rw link-id            link-id
       ....................................................
       +--rw ex:foo-link!
       +--rw tet:te!
          +--rw te-link-attributes
             +--rw interface-switching-capability*
             |       [switching-capability encoding]
             |  +--rw switching-capability    identityref
             |  +--rw encoding                identityref
             ..............................................
             +--rw ex:bar-node
                ...........................................
~~~~

This approach gives implementation freedom to instantiate or not the te-topology for non-TE network types.

It is also possible to define a non-presence container under the te-link-attributes to group the attributes for a node that supports a given TE layer.

A single layer link has only one link presence container or a single instance in the interface-switching-capability list. A multi-layer node has multiple link presence containers, one for each non-TE layer it can support, or multiple instances in the interface-switching-capability list, one for each TE layer it can support.

A multi-layer link can also support a mix of TE and non-TE layers.

## LTP Type

To be added

~~~~
    +--rw nt:termination-point* [tp-id]
       +--rw tp-id                           tp-id
       ....................................................
       +--rw foo-tp!
       +--rw tet:te-tp-id?   te-types:te-tp-id
       +--rw tet:te!
          +--rw interface-switching-capability*
          |       [switching-capability encoding]
          |  +--rw switching-capability    identityref
          |  +--rw encoding                identityref
          .................................................
          +--rw ex:baz-tp
             ..............................................
~~~~

## Label Range

To be added

~~~~
    +--rw tet:label-restrictions
       +--rw label-restriction* [index]
          +--rw restriction?    enumeration
          +--rw index           uint32
          +--rw ex:bar-label-range!
          +--rw ex:baz-label-range!
          +--rw label-start
          |  +--rw te-label
          |     +--rw (technology)?
          |     |  ........................................
          |     |  +--:(ex:bar)
          |     |  |  +--rw bar-label
          |     |  |     ..................................
          |     |  +--:(ex:baz)
          |     |     +--rw baz-label
          |     |        ..................................
          |     +--rw direction?       te-label-direction
          +--rw label-end
          |  +--rw te-label
          |     +--rw (technology)?
          |     |  ........................................
          |     |  +--:(ex:bar)
          |     |  |  +--rw bar-label
          |     |  |     ..................................
          |     |  +--:(ex:baz)
          |     |     +--rw baz-label
          |     |        ..................................
          |     +--rw direction?       te-label-direction
          +--rw label-step
          |  +--rw (technology)?
          |     ...........................................
          |     +--:(ex:bar)
          |     |  +--rw bar-label-step
          |     |     .....................................
          |     +--:(ex:baz)
          |        +--rw baz-label-step
          |           .....................................
          +--rw range-bitmap?   yang:hex-string
~~~~

Note 1: the label-range presence containers are mutually exclusive even if it is not possible to express this using the YANG syntax.

Note 2: the use of the (technology) choice with the when statements should be reconsidered based on the on-going discussion in Netmod WG regarding RFC8407-bis.

## Bandwidth

To be added

~~~~
       +--rw tet:te-bandwidth
          +--rw (technology)?
          +--rw ex:bar-bandwidth
          |   ................................
          +--rw ex:baz-bandwidth
              ................................
~~~~

The (technology) choice is not used to allow expressing the different bandwidth information, one for each supported layer, in case of multi-layer links
