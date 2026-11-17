PATIL WATER PARK WEBSITE
========================

FILES
- index.html: responsive customer website and booking form
- supabase_schema.sql: database tables and secure booking RPC

SETUP
1. Open Supabase project: https://kepkgwoyecwvqbvxupib.supabase.co
2. Go to SQL Editor > New query.
3. Paste all contents of supabase_schema.sql and click Run.
4. In GitHub, open your website repository, replace index.html with this index.html, and commit.
5. Enable GitHub Pages in repository Settings > Pages if not already enabled.
6. Test one booking with a future date and a valid UPI reference.

PAYMENT IMPORTANT
The website opens a UPI payment app using your UPI ID. The customer enters the UTR/reference.
This is NOT automatic payment verification. Bookings remain pending until you verify the payment
in your UPI/bank app. Do not mark a booking paid based only on the customer's typed reference.
For automatic payment confirmation, integrate a payment gateway such as Razorpay with server-side
webhooks and secret keys stored only in Supabase Edge Functions, never in index.html.

ADMIN
The current package creates the secure database and customer booking flow. It intentionally does
not expose customer booking records publicly. Create an admin user in Supabase Authentication,
then add that user's UUID to waterpark_admins using the SQL comment in supabase_schema.sql.
An authenticated admin dashboard / payment verification workflow is a separate next build step.

EDIT BEFORE LAUNCH
- Add the park's full address, official contact/WhatsApp number, and child age definition.
- Confirm the exact operating days and whether all dates are bookable.
- Confirm whether child ticket age limit is below 10 (not assumed in this build).
- Replace sample Unsplash photos with approved real park photographs if available.

SECURITY
The Supabase publishable key is intended for browser use. Never put a service_role or secret key
in the website. Keep Row Level Security enabled. The booking RPC validates inputs and locks
the date capacity row to prevent concurrent bookings from exceeding 1,000 visitors/day.
