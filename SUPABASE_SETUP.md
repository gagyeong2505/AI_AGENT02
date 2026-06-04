# Supabase setup

## 1. Create storage bucket

Create a public Storage bucket named `COURSE-FILES`.

## 2. Create instructor account

In Supabase Authentication, create the instructor email/password account used for uploads.

## 3. Add storage policies

Run these policies in Supabase SQL Editor.

```sql
create policy "course files are readable"
on storage.objects
for select
to anon, authenticated
using (bucket_id = 'COURSE-FILES');

create policy "authenticated users can upload course files"
on storage.objects
for insert
to authenticated
with check (bucket_id = 'COURSE-FILES');
```

## 4. Configure the site

Edit `supabase-config.js`, then replace `url` and `anonKey`.

For GitHub Pages deployment, commit `supabase-config.js` too. The anon key is designed for browser use, but never add a service role key.
