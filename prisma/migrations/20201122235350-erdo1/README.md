# Migration `20201122235350-erdo1`

This migration has been generated at 11/23/2020, 12:53:50 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "User" (
    "email" TEXT NOT NULL,
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" TEXT
)

CREATE TABLE "Hospital" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL,
    "address" TEXT NOT NULL
)

CREATE TABLE "Post" (
    "authorId" INTEGER,
    "content" TEXT,
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "published" BOOLEAN NOT NULL DEFAULT false,
    "title" TEXT NOT NULL,

    FOREIGN KEY ("authorId") REFERENCES "User"("id") ON DELETE SET NULL ON UPDATE CASCADE
)

CREATE UNIQUE INDEX "User.email_unique" ON "User"("email")
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20201122235350-erdo1
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,30 @@
+generator client {
+  provider = "prisma-client-js"
+}
+
+datasource db {
+  provider = "sqlite"
+  url = "***"
+}
+
+model User {
+  email String  @unique
+  id    Int     @id @default(autoincrement())
+  name  String?
+  posts Post[]
+}
+
+model Hospital {
+  id      Int    @id @default(autoincrement())
+  name    String
+  address String
+}
+
+model Post {
+  authorId  Int?
+  content   String?
+  id        Int     @id @default(autoincrement())
+  published Boolean @default(false)
+  title     String
+  author    User?   @relation(fields: [authorId], references: [id])
+}
```


