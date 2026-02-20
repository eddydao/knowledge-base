Temporary disable foreign key in postgresql:
`SET session_replication_role = 'replica';`

Return the foreign keys into normal mode
`SET session_replication_role = 'origin';`