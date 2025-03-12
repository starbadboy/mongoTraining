# MongoDB Training Notes

## Overview
This repository contains comprehensive notes from MongoDB MDB100 and MDB200 training courses. The notes are organized into modules that cover MongoDB fundamentals and advanced topics.

## Contents

### Core Modules
- [MDB100 - MongoDB Basics](MDB100.md)
  - Introduction to MongoDB and Atlas
  - Storage and Retrieval Part 1
  - Storage and Retrieval Part 2
  - Security

- [MDB200 - MongoDB Advanced Topics](MDB200.md)
  - Indexes and Optimization Part 1
  - Indexes and Optimization Part 2
  - Finding Slow Operations with Logs and Metrics
  - Intro to Atlas Search and Atlas Vector Search

### Visual Aids
- [MDB100 Key Concepts Diagrams](MDB100_Diagram.md)
- [MDB200 Key Concepts Diagrams](MDB200_Diagram.md)

### Reference Materials
- [MongoDB Command Cheatsheet](MongoDB_Cheatsheet.md)
- [MongoDB Glossary](MongoDB_Glossary.md)

## How to Use These Notes

### For Beginners
If you're new to MongoDB, start with the MDB100 module notes. These cover the fundamental concepts of MongoDB, including:
- Document model
- Basic CRUD operations
- Query language
- Aggregation framework
- Security basics

### For Intermediate Users
After mastering the basics, proceed to the MDB200 module notes, which cover:
- Advanced indexing strategies
- Query optimization
- Performance monitoring and troubleshooting
- Atlas Search and Vector Search capabilities

### Quick Reference
- Use the Command Cheatsheet for quick syntax reference
- Refer to the Glossary for clarification on MongoDB terminology
- Browse the diagram files for visual representations of key concepts

## Key Takeaways

1. **Document Model**: MongoDB's flexible document model allows for natural representation of hierarchical data without complex joins.

2. **Performance Optimization**: Proper indexing is critical for MongoDB performance. Create indexes that support your query patterns, and use the explain plan to verify query execution.

3. **Monitoring Best Practices**: 
   - Keep cache hit ratio around 80%
   - Monitor replication lag
   - Set swappiness to 1 to minimize swap usage
   - Watch for CPU, memory, and disk I/O bottlenecks

4. **Atlas Capabilities**: MongoDB Atlas provides managed database services with built-in monitoring, backups, security features, and advanced capabilities like Atlas Search and Vector Search.

## Additional Resources

- [MongoDB Documentation](https://docs.mongodb.com/)
- [MongoDB University](https://university.mongodb.com/)
- [MongoDB Developer Center](https://mongodb.com/developer/)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) 