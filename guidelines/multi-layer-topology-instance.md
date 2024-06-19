# Guidelines for multi-layer topology instance

## Network Type

The network-types presence container has been defined to support different types of networks as described in section 2.4.4 of \[RFC8345]

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

It is worth noting that presence containers for TE network-types (i.e., those topology models which augment the TE Topology model of \[RFC8795]) are instantiated within the te-topology presence container, while the presence containers for non-TE network-types (i.e., those topology models which do not augment the TE Topology model of \[RFC8795]) are instantiated outside the te-topology presence container.

In principle, it would be possible to instantiate presence containers for non-TE network-types in a hierarchical structure, like the one used between TE topology and TE network types: in this case a non-TE topology model is augmenting another non-TE topology model.

## Node Type

A multi-layer topology instance can contains nodes which support one or multiple layers.

In order to report which layer(s) a node can support, presence containers are defined under the node to indicate whether the node supports a given layer.

The structure of these presence containers, is aligned with the principles used for network-types:

- for non-TE network types, the presence containers are defined under the node;

- for TE network-types, the presence containers are defined under the te-node-attributes container.

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

In order to report which layer(s) a link can support, presence containers are, in general, defined under the link to indicate whether the link supports a given layer.

The structure of these presence containers, is aligned with the principles used for network-types:

- for non-TE network types, the presence containers are defined under the link;

- for TE network-types, the presence containers are, in general, defined under the link. However, if the network-types is represented by interface-switching-capability, the interface-switching-capability list, already defined in \[RFC8795] for the same purpose, shall be used instead of defining a presence container.

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
             +--rw ex:bar-link
             |  ...........................................
             +--rw ex:baz-link!
~~~~

This approach gives implementation freedom to instantiate or not the te-topology for non-TE network types.

It is also possible to define a non-presence container under the te-link-attributes to group the attributes for a node that supports a given TE layer, represented by interface-switching-capability.

A single layer link has only one link presence container or a single instance in the interface-switching-capability list. A multi-layer node has multiple link presence containers or multiple instances in the interface-switching-capability list, one for each layer it can support.

A multi-layer link can also support a mix of TE and non-TE layers.

## LTP Type

A multi-layer topology instance can contains link termination points (LTPs) which support one or multiple layers.

When an LTP terminates one or more links, it is implicitly assumed that the LTP can support all the layers of the links it terminates.

In this case there is no need to provide any additional information about which layer(s) an LTP can support.

However, when an LTP does not terminate any link, there is a need to report which layer(s) an LTP can support. In this case, the same rules defined for the link applies:

~~~~
    +--rw nt:termination-point* [tp-id]
       +--rw tp-id                           tp-id
       ....................................................
       +--rw ex:foo-tp!
       +--rw tet:te-tp-id?   te-types:te-tp-id
       +--rw tet:te!
          +--rw interface-switching-capability*
          |       [switching-capability encoding]
          |  +--rw switching-capability    identityref
          |  +--rw encoding                identityref
          .................................................
          +--rw ex:baz-tp
          |  ...........................................
          +--rw ex:baz-tp!
~~~~

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
             +--rw ex:bar-link
             |  ...........................................
             +--rw ex:baz-link!
~~~~


## Label Range

A multi-layer link supports different technology-specific label ranges for different layers.

While each entry in the label-restriction list specify a label range for a single layer, multiple entries in the label-restriction list can specify label ranges for multiple layers.

A presence container can be define to indicate to which layer a given label range entry applies.

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

A multi-layer link supports different technology-specific bandwidth definitions for different layers.

Different containers, one for each layer, can be defined under the te-bandwidth container to represent the bandwidth for each layer supported by the link:

~~~~
       +--rw tet:te-bandwidth
          +--rw (technology)?
          +--rw ex:bar-bandwidth
          |   ................................
          +--rw ex:baz-bandwidth
              ................................
~~~~

The (technology) choice is not used in order to allow expressing the different bandwidth information, one for each supported layer, in case of multi-layer links
