# Prisma Install with Next.js + NeonDB

---

## ১. Next.js Installation

নতুন Next.js প্রজেক্ট তৈরি করো এবং সেই ডিরেক্টরিতে প্রবেশ করো:

```bash
npx create-next-app@latest prisma-schema
cd prisma-schema
```

---

## ২. Prisma Dependencies Install

### Dev dependencies:
```bash
npm install prisma tsx @types/pg --save-dev
```

### Production dependencies:
```bash
npm install @prisma/client @prisma/adapter-pg dotenv pg
```

---

## ৩. Prisma Initialize করো

```bash
npx prisma init --output ../app/generated/prisma
```

এই কমান্ড চালালে যা তৈরি হবে:

| ফাইল / ডিরেক্টরি | বিবরণ |
|---|---|
| `prisma/schema.prisma` | Prisma schema ফাইল |
| `prisma.config.ts` | Prisma কনফিগারেশন ফাইল |
| `.env` | `DATABASE_URL` সহ environment file |
| `app/generated/prisma/` | Generated Prisma Client (পরে তৈরি হবে) |

> ⚠️ `app/generated/prisma` ডিরেক্টরি তখনই তৈরি হবে যখন `prisma generate` অথবা `prisma migrate dev` রান করবে।

---

## ৪. NeonDB Database তৈরি করো

### ধাপে ধাপে NeonDB সেটআপ:

**ধাপ ১ — NeonDB তে যাও:**
👉 [https://neon.tech](https://neon.tech) ভিজিট করো → **Sign Up** করো → **Login** করো

**ধাপ ২ — নতুন প্রজেক্ট তৈরি করো:**

| ফিল্ড | মান |
|---|---|
| Project Name | `Prisma Project` |
| Region | `AWS Asia Pacific 1 (Singapore)` |

তারপর **Create** বাটনে ক্লিক করো।

**ধাপ ৩ — Connection String কপি করো:**

```
Dashboard → Connect → Copy snippet
```

**ধাপ ৪ — `.env` ফাইলে পেস্ট করো:**

```env
DATABASE_URL="postgresql://username:password@ep-xxx.ap-southeast-1.aws.neon.tech/neondb?sslmode=require"
```

> ✅ NeonDB থেকে কপি করা `postgres://...` string টি `DATABASE_URL` এর মান হিসেবে বসাও।

---

## ৫. Migration চালাও এবং Prisma Client Generate করো

```bash
npx prisma migrate dev --name init
npx prisma generate
```

| কমান্ড | কাজ |
|---|---|
| `prisma migrate dev --name init` | NeonDB-তে table তৈরি করে এবং migration history রাখে |
| `prisma generate` | Prisma Client কোড generate করে |

---

## ৬. NeonDB Dashboard এ Table Verify করো

NeonDB Dashboard এ গিয়ে table তৈরি হয়েছে কিনা চেক করো:

```
Neon Dashboard → Tables → তোমার table এর নাম দেখো
```

> ✅ যদি table দেখতে পাও, তাহলে সেটআপ সফলভাবে সম্পন্ন হয়েছে!

---

## Quick Summary

```
create-next-app
      ↓
npm install (prisma, pg, client)
      ↓
prisma init
      ↓
neon.tech → New Project → Connect → Copy snippet
      ↓
.env তে DATABASE_URL পেস্ট
      ↓
prisma migrate dev
      ↓
prisma generate
      ↓
Neon Dashboard → Tables → verify ✅
```
