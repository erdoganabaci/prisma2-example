# Migration `20201123003458-adres`

This migration has been generated at 11/23/2020, 1:34:58 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "Hospital" ADD COLUMN     "address" TEXT
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201123001419-test2..20201123003458-adres
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
   email    String     @unique
@@ -15,12 +15,13 @@
   hospital Hospital[]
 }
 model Hospital {
-  id     Int    @id @default(autoincrement())
-  name   String
-  User   User?  @relation(fields: [userId], references: [id])
-  userId Int?
+  id      Int     @id @default(autoincrement())
+  name    String
+  address String?
+  User    User?   @relation(fields: [userId], references: [id])
+  userId  Int?
 }
 model Post {
   authorId  Int?
```


