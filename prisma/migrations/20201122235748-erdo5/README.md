# Migration `20201122235748-erdo5`

This migration has been generated at 11/23/2020, 12:57:48 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;
CREATE TABLE "new_Hospital" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL
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
migration 20201122235532-erdo3..20201122235748-erdo5
--- datamodel.dml
+++ datamodel.dml
@@ -3,9 +3,9 @@
 }
 datasource db {
   provider = "sqlite"
-  url = "***"
+  url = "***"
 }
 model User {
   email String  @unique
@@ -14,11 +14,10 @@
   posts Post[]
 }
 model Hospital {
-  id      Int    @id @default(autoincrement())
-  name    String
-  address String
+  id   Int    @id @default(autoincrement())
+  name String
 }
 model Post {
   authorId  Int?
```


