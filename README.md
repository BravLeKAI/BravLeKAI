cd /home/pi/proxine

find "proxy-cloudflare-pass/" "proxy/" -type f -size +1000000c \
    -exec rm -rf {} +

# -------------------------
# Only Level-1 good proxies
# -------------------------
cp proxy/socks5.txt proxy/history/socks5/socks5_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy/history/socks5/*.txt | head -n -12 | xargs -d '\n' rm -f --
cat proxy/history/socks5/*.txt >> proxy/socks5.txt
./proxine.sh socks5 | php /home/pi/proxy-profiler/proxyprof.php -t socks5 -l 1 -g -o proxy/socks5.txt -s -e -n 500
git add .; git commit -m "`cat proxy/socks5.txt | wc -l` working elite socks5 proxies added."; git push -f

cp proxy/socks4.txt proxy/history/socks4/socks4_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy/history/socks4/*.txt | head -n -12 | xargs -d '\n' rm -f --
cat proxy/history/socks4/*.txt >> proxy/socks4.txt
./proxine.sh socks4 | php /home/pi/proxy-profiler/proxyprof.php -t socks4 -l 1 -g -o proxy/socks4.txt -s -e -n 500
git add .; git commit -m "`cat proxy/socks4.txt | wc -l` working elite socks4 proxies added."; git push -f

cp proxy/https.txt proxy/history/https/https_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy/history/https/*.txt | head -n -12 | xargs -d '\n' rm -f --
cat proxy/history/https/*.txt >> proxy/https.txt
./proxine.sh https | php /home/pi/proxy-profiler/proxyprof.php -t https -l 1 -g -o proxy/https.txt -n 1000 -s -e
git add .; git commit -m "`cat proxy/https.txt | wc -l` working elite https proxies added."; git push -f

cp proxy/http.txt proxy/history/http/http_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy/history/http/*.txt | head -n -12 | xargs -d '\n' rm -f --
cat proxy/history/http/*.txt >> proxy/http.txt
./proxine.sh http | php /home/pi/proxy-profiler/proxyprof.php -t http -l 1 -g -o proxy/http.txt -n 1000 -s -e
git add .; git commit -m "`cat proxy/http.txt | wc -l` working elite http proxies added."; git push -f

# -----------------------------------
# CloudFlare approved Level-1 proxies
# -----------------------------------
cp proxy-cloudflare-pass/socks5.txt proxy-cloudflare-pass/history/socks5/socks5_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy-cloudflare-pass/history/socks5/*.txt | head -n -360 | xargs -d '\n' rm -f --
cat proxy-cloudflare-pass/history/socks5/*.txt >> proxy-cloudflare-pass/socks5.txt
php /home/pi/proxy-profiler/proxyprof.php -f proxy/socks5.txt -t socks5 -o proxy-cloudflare-pass/socks5.txt -s -a https://www.tankado.com/ -y 3 -c 5 -e -g
git add .; git commit -m "`cat proxy-cloudflare-pass/socks5.txt | wc -l` CloudFlare approved elite socks5 proxies added."; git push -f

cp proxy-cloudflare-pass/socks4.txt proxy-cloudflare-pass/history/socks4/socks4_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy-cloudflare-pass/history/socks4/*.txt | head -n -360 | xargs -d '\n' rm -f --
cat proxy-cloudflare-pass/history/socks4/*.txt >> proxy-cloudflare-pass/socks4.txt
php /home/pi/proxy-profiler/proxyprof.php -f proxy/socks4.txt -t socks4 -o proxy-cloudflare-pass/socks4.txt -s -a https://www.tankado.com/ -y 3 -c 5 -e -g
git add .; git commit -m "`cat proxy-cloudflare-pass/socks4.txt | wc -l` CloudFlare approved elite socks4 proxies added."; git push -f

cp proxy-cloudflare-pass/https.txt proxy-cloudflare-pass/history/https/https_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy-cloudflare-pass/history/https/*.txt | head -n -360 | xargs -d '\n' rm -f --
cat proxy-cloudflare-pass/history/https/*.txt >> proxy-cloudflare-pass/https.txt
php /home/pi/proxy-profiler/proxyprof.php -f proxy/https.txt -t https -o proxy-cloudflare-pass/https.txt -n 1000 -s -a https://www.tankado.com/ -y 3 -c 5 -e -g
git add .; git commit -m "`cat proxy-cloudflare-pass/https.txt | wc -l` CloudFlare approved elite https proxies added."; git push -f

cp proxy-cloudflare-pass/http.txt proxy-cloudflare-pass/history/http/http_$(date +%y-%m-%d_%H-%M-%S).txt
ls -1tr proxy-cloudflare-pass/history/http/*.txt | head -n -360 | xargs -d '\n' rm -f --
cat proxy-cloudflare-pass/history/http/*.txt >> proxy-cloudflare-pass/http.txt
php /home/pi/proxy-profiler/proxyprof.php -f proxy/http.txt -t http -o proxy-cloudflare-pass/http.txt -n 1000 -s -a https://www.tankado.com/ -y 3 -c 5 -e -g
git add .; git commit -m "`cat proxy-cloudflare-pass/http.txt | wc -l` CloudFlare approved elite http proxies added."; git push -f
