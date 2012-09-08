---
title: 'TriangleJS Notes For 2012-07-24: Graph Database'
created_at: 2012-07-24 23:10:00 UTC
---

"Data are from Mars, RDBMs are from Venus."

## Non-relational Databases

CouchDB
Cassandra
redis
MondoDB
riak

## Graph Databases

OrientDB
Neo4J
Flock (Twitter)
others...

## Graphs are everywhere:

* street maps
* computer network
* social network
* relational databases
  * records == nodes
  * foreign keys == edges
  * ORMs translate to in-memory graph
* whiteboard friendly
* natural language processing
  * nouns == nodes
  * verbs == relationships
* access control list
* LinkIn uses Neo4J to find relations on the fly
* Twitter uses custom-built graph database
* FrostyMug beer recommendation engine

## Neo4J

* RESTful interface
* ACID complient
* High availability
* Scalable
* AGPL licenced
* http://console.neo4j.org/
* Lucene indexing engine by default
* Each node is an arbitrary bag of properties
  * Edges are special nodes with two properties (left,right)
  * Not really types that Neo4J, need to be managed by application
  * Which index a node is in can determine it's "type"
* Jeff is a graph serialization format
* Cypher is a query language proposal by Neo4J

## Cypher Queries Examples

    # http://tinyurl.com/c65d99w
    # Kevin Bacon
    START s=node:actors(name="Keanu Reeves"),
          e=node:actors(name="Kevin Bacon")
    MATCH p = shortestPath(s-[*]-e)
    RETURN p, length(p)


    # http://tinyurl.com/cyn3rkx
    # no need to worry about nested sub-groups

    # start with user 3
    START u=node:users(name="User 3")

    # find all groups the user(s) is in
    MATCH u-[:belongs_to*]->g

    # return group(s) that user 3 is in
    RETURN g


    # http://tinyurl.com/dx7onro
    START u=node:users(name="User 3"),
          o=node:objects(name="Home")
    # find zero or more belongs_to relationships
    # that can_read the home page
    # for user 1, g is u (zero or more...)
    MATCH u-[:belongs_to*0..]->g,
          g-[:can_read]->o
    RETURN g


    # http://tinyurl.com/bwtyhvt
    START u=node:users(name="User 3"),
          o=node:objects(name="Home")
    MATCH u-[:belongs_to*0..]->g,
          g-[:can_read]->o,
          # optional denied relationship
          u-[d?:denied*]->o
    WHERE d is null
    RETURN g

## Resturant Example

Companies have brands, locations, location groups
Brands have locations, location groups
Location groups have locations


      # http://tinyurl.com/cxm4heh
      START c=node:companies(name="Company 1")
      MATCH c-[:HAS*]->1
      WHERE l.type = 'location'
      RETURN l
      ORDER BY l.name


      # http://tinyurl.com/cl537w6
      START b=node(3)
      MATCH b<-[:HAS*]-c-[:HAS*]->l<-[h?:HAS*]-b
      WHERE h IS NULL AND l.type='location'
      RETURN l
      ORDER BY l.name
