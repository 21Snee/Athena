git clone https://github.com/fdarkaou/anotherwrapper-premium.git Athena
cd Athena
git remote remove origin

cat <<EOT > .env.local
PRODUCTION_URL=https://localhost:3000
NEXT_PUBLIC_SUPABASE_URL=xyz
NEXT_PUBLIC_SUPABASE_ANON_KEY=xyz
NEXT_SUPABASE_SERVICE_KEY=xyz
PORT=3000
EOT

cat <<EOT > setup.sh
#!/bin/bash
echo "Running setup.sh"
npm install
npm run build
echo "Setup complete"
EOT

chmod +x setup.sh
./setup.sh

if lsof -i :3000; then
  kill -9 $(lsof -t -i :3000)
fi

npm run dev
// next.config.js
console.log('NEXT_PUBLIC_SUPABASE_URL:', process.env.NEXT_PUBLIC_SUPABASE_URL);

