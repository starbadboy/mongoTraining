# MDB200 Key Concepts Diagram

## MongoDB Indexing Strategy

```
┌───────────────────────────────────────────────────────────┐
│                   Indexing Strategy                        │
└───────────────────────────┬───────────────────────────────┘
                            │
          ┌────────────────┴────────────────┐
          ▼                                 ▼
┌─────────────────────┐          ┌─────────────────────────┐
│    Query Patterns   │          │    Data Characteristics  │
│                     │          │                         │
│ • Equality vs Range │          │ • Cardinality          │
│ • Sort Requirements │          │ • Document Size        │
│ • Covered Queries   │          │ • Update Frequency     │
│ • Frequency         │          │ • Working Set Size     │
└──────────┬──────────┘          └─────────────┬───────────┘
           │                                   │
           └────────────────┬─────────────────┘
                            │
                            ▼
┌───────────────────────────────────────────────────────────┐
│                   Index Selection                          │
│                                                           │
│  ┌───────────────┐   ┌──────────────┐   ┌──────────────┐  │
│  │ Single Field  │   │  Compound    │   │ Special      │  │
│  │               │   │              │   │ Purpose      │  │
│  │ • Simple      │   │ • Multiple   │   │ • Text       │  │
│  │   Queries     │   │   Fields     │   │ • Geospatial │  │
│  │ • Low         │   │ • Sort +     │   │ • Hashed     │  │
│  │   Overhead    │   │   Filter     │   │ • TTL        │  │
│  └───────────────┘   └──────────────┘   └──────────────┘  │
└───────────────────────────────────────────────────────────┘
```

## MongoDB Query Execution and Optimization

```
┌───────────────────────┐
│      Query Entry      │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│    Query Parsing      │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│   Query Planning      │
│                       │
│  ┌─────────────────┐  │
│  │Plan Generation  │  │
│  └─────┬───────────┘  │
│        │              │
│  ┌─────▼───────────┐  │
│  │Plan Selection   │  │
│  └─────┬───────────┘  │
│        │              │
│  ┌─────▼───────────┐  │
│  │ Plan Caching    │  │
│  └─────────────────┘  │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│   Query Execution     │
│                       │
│  ┌─────────────────┐  │
│  │ COLLSCAN        │  │
│  │ (No Index)      │  │
│  └─────────────────┘  │
│  ┌─────────────────┐  │
│  │ IXSCAN          │  │
│  │ (Using Index)   │  │
│  └─────────────────┘  │
│  ┌─────────────────┐  │
│  │ FETCH           │  │
│  │ (Get Documents) │  │
│  └─────────────────┘  │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│   Results Returned    │
└───────────────────────┘
```

## MongoDB Performance Monitoring and Troubleshooting

```
┌────────────────────────────────────────────────────────────┐
│                 MongoDB Performance Monitoring              │
└─────────────────────────────┬──────────────────────────────┘
                              │
     ┌──────────────────────┬─┴─────────────┬───────────────┐
     ▼                      ▼               ▼               ▼
┌──────────────┐    ┌───────────────┐ ┌───────────┐  ┌───────────────┐
│System Metrics│    │MongoDB Metrics│ │Profiling &│  │Query Patterns │
│              │    │               │ │Logging    │  │               │
│• CPU         │    │• Operation    │ │           │  │• Slow Queries │
│• Memory      │    │  Counters     │ │• Profile  │  │• Missing      │
│• Disk I/O    │    │• Cache Hit    │ │  Level    │  │  Indexes      │
│• Swappiness  │    │  Ratio        │ │• Log      │  │• Inefficient  │
│  (set to 1)  │    │• Connections  │ │  Analysis │  │  Query Design │
└──────┬───────┘    │• Replication  │ │• Current  │  └───────┬───────┘
       │            │  Lag          │ │  Op       │          │
       │            └───────┬───────┘ └─────┬─────┘          │
       │                    │               │                │
       └──────────┬─────────┴───────────────┴────────┬──────┘
                  │                                  │
                  ▼                                  ▼
   ┌───────────────────────────┐        ┌─────────────────────────────┐
   │ Performance Issues        │        │      Solutions              │
   │                           │        │                             │
   │ • Missing Indexes         │ ─────► │ • Create Proper Indexes     │
   │ • Inefficient Queries     │ ─────► │ • Rewrite Queries          │
   │ • Resource Constraints    │ ─────► │ • Upgrade/Scale Resources   │
   │ • Working Set > RAM       │ ─────► │ • Increase Memory/Sharding  │
   │ • Long-Running Operations │ ─────► │ • Identify & Kill Operations│
   │ • Lock Contention         │ ─────► │ • Optimize Query Patterns   │
   └───────────────────────────┘        └─────────────────────────────┘
```

## Atlas Search and Vector Search Architecture

```
┌───────────────────────────────────────────────────────────────┐
│                     MongoDB Atlas                              │
│                                                               │
│  ┌───────────────────────────────────────────────────────┐   │
│  │                   Database Cluster                     │   │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐   │   │
│  │  │ Primary │  │Secondary│  │Secondary│  │Secondary│   │   │
│  │  │  Node   │  │  Node   │  │  Node   │  │  Node   │   │   │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘   │   │
│  └───────────────────────────────────────────────────────┘   │
│                              │                                │
│                              │ Replication                    │
│                              ▼                                │
│  ┌───────────────────────────────────────────────────────┐   │
│  │                  Dedicated Search Nodes                │   │
│  │  ┌─────────────────┐        ┌─────────────────┐       │   │
│  │  │ Search Node 1   │        │ Search Node 2   │       │   │
│  │  │                 │        │                 │       │   │
│  │  │ ┌─────────────┐ │        │ ┌─────────────┐ │       │   │
│  │  │ │ Atlas Search│ │        │ │ Atlas Search│ │       │   │
│  │  │ │  (Apache    │ │        │ │  (Apache    │ │       │   │
│  │  │ │   Lucene)   │ │        │ │   Lucene)   │ │       │   │
│  │  │ └─────────────┘ │        │ └─────────────┘ │       │   │
│  │  │                 │        │                 │       │   │
│  │  │ ┌─────────────┐ │        │ ┌─────────────┐ │       │   │
│  │  │ │ Vector      │ │        │ │ Vector      │ │       │   │
│  │  │ │ Search      │ │        │ │ Search      │ │       │   │
│  │  │ └─────────────┘ │        │ └─────────────┘ │       │   │
│  │  └─────────────────┘        └─────────────────┘       │   │
│  └───────────────────────────────────────────────────────┘   │
└───────────────────────────────────────────────────────────────┘
```

## RAG (Retrieval-Augmented Generation) with MongoDB Vector Search

```
┌────────────────────────────────────────────────────────────────┐
│                RAG Architecture with MongoDB                    │
└──────────────────────────────┬─────────────────────────────────┘
                               │
     ┌─────────────────────────┼──────────────────────┐
     ▼                         ▼                      ▼
┌─────────────┐         ┌─────────────┐        ┌─────────────┐
│ Document    │         │ Query       │        │ Response    │
│ Processing  │         │ Processing  │        │ Generation  │
└──────┬──────┘         └──────┬──────┘        └──────┬──────┘
       │                       │                      │
       ▼                       ▼                      ▼
┌─────────────┐         ┌─────────────┐        ┌─────────────┐
│ 1. Document │         │ 1. User     │        │ 1. Combine  │
│    Ingestion│         │    Query    │        │    Context  │
└──────┬──────┘         └──────┬──────┘        └──────┬──────┘
       │                       │                      │
       ▼                       ▼                      ▼
┌─────────────┐         ┌─────────────┐        ┌─────────────┐
│ 2. Generate │         │ 2. Generate │        │ 2. Generate │
│    Embedding│         │    Embedding│        │    Response │
└──────┬──────┘         └──────┬──────┘        └─────────────┘
       │                       │                      ▲
       ▼                       ▼                      │
┌─────────────┐         ┌─────────────┐              │
│ 3. Store in │         │ 3. Vector   │              │
│    MongoDB  │────────►│    Search   │──────────────┘
└─────────────┘         └─────────────┘
``` 