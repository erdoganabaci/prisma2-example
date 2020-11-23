# Migration `20201123001419-test2`

This migration has been generated at 11/23/2020, 1:14:19 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;
CREATE TABLE "new_Hospital" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL,
    "userId" INTEGER,

    FOREIGN KEY ("userId") REFERENCES "User"("id") ON DELETE SET NULL ON UPDATE CASCADE
);
INSERT INTO "new_Hospital" ("id", "name") SELECT "id", "name" FROM "Hospital";
DROP TABLE "Hospital";
ALTER TABLE "new_Hospital" RENAME TO "Hospital";
PRAGMA foreign_key_check;
PRAGMA foreign_keys=ON
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201122235748-erdo5..20201123001419-test2
--- datamodel.dml
+++ datamodel.dml
@@ -3,21 +3,24 @@
 }
 datasource db {
   provider = "sqlite"
-  url = "***"
+  url = "***"
 }
 model User {
-  email String  @unique
-  id    Int     @id @default(autoincrement())
-  name  String?
-  posts Post[]
+  email    String     @unique
+  id       Int        @id @default(autoincrement())
+  name     String?
+  posts    Post[]
+  hospital Hospital[]
 }
 model Hospital {
-  id   Int    @id @default(autoincrement())
-  name String
+  id     Int    @id @default(autoincrement())
+  name   String
+  User   User?  @relation(fields: [userId], references: [id])
+  userId Int?
 }
 model Post {
   authorId  Int?
```


