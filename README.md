# Inventory System

## 🚀 About the Project

 Inventory Management System using **Laravel**, designed to streamline stock tracking, reduce errors, and enhance operational efficiency. This system enables businesses to efficiently manage product inventory, monitor stock levels, and automate key inventory processes. 

---

## 🛠️ Tech Stack

- **Frontend:** Laravel Blade
- **Backend:** PHP
- **Database:** MySQL (MariaDB can be used)
- **Deployment:** VPS with Nginx or Apache

---

## ✨ Features

- Fully responsive design with Bootstrap 5
- High data accuracy with trigger and functions

---

## 📁 Project Structure

```sh
inventory-system/
├── app
│   ├── Http
│   │   └── Controllers
│   │       ├── control_barang.php
│   │       ├── control_dashboard.php
│   │       ├── control_kategori.php
│   │       ├── control_keluar.php
│   │       ├── control_masuk.php
│   │       └── Controller.php
│   ├── Models
│   │   ├── model_barang.php
│   │   ├── model_kategori.php
│   │   ├── model_keluar.php
│   │   ├── model_masuk.php
│   │   └── User.php
│   └── Providers
│       └── AppServiceProvider.php
├── bootstrap/
├── config/
├── database
│   ├── factories
│   │   └── UserFactory.php
│   ├── migrations
│   │   ├── 0001_01_01_000000_create_users_table.php
│   │   ├── 0001_01_01_000001_create_cache_table.php
│   │   ├── 0001_01_01_000002_create_jobs_table.php
│   │   ├── 2025_01_02_101232_tabel_kategori.php
│   │   ├── 2025_02_16_113038_create_barang_table.php
│   │   ├── 2025_02_16_113054_create_barang_masuk_table.php
│   │   ├── 2025_02_16_113103_create_barang_keluar_table.php
│   │   ├── 2025_07_03_045347_trigger_masuk.php
│   │   ├── 2025_07_03_045351_trigger_keluar.php
│   │   └── 2025_07_03_045816_function_barang.php
│   ├── seeders
│   │   └── DatabaseSeeder.php
│   └── .gitignore
├── public/
│   ├── .htaccess
│   ├── favicon.ico
│   ├── index.php
│   └── robots.txt
├── resources
│   ├── css
│   │   └── app.css
│   ├── js
│   │   ├── app.js
│   │   └── bootstrap.js
│   └── views
│       └── frontend
│           ├── barang
│           │   ├── create.blade.php
│           │   ├── edit.blade.php
│           │   ├── index.blade.php
│           │   └── show.blade.php
│           ├── dashboard
│           │   └── index.blade.php
│           ├── kategori
│           │   ├── create.blade.php
│           │   ├── delete.blade.php
│           │   ├── edit.blade.php
│           │   ├── index.blade.php
│           │   └── show.blade.php
│           ├── keluar
│           │   ├── create.blade.php
│           │   ├── edit.blade.php
│           │   ├── index.blade.php
│           │   └── show.blade.php
│           ├── layout
│           │   └── layout-crud.blade.php
│           └── masuk
│               ├── create.blade.php
│               ├── edit.blade.php
│               ├── index.blade.php
│               └── show.blade.php
├── routes
│   ├── console.php
│   └── web.php
├── .editorconfig
├── .env.example
├── .gitattributes
├── .gitignore
├── artisan
├── composer.json
├── composer.lock
├── package.json
├── phpunit.xml
├── postcss.config.js
├── README.md
├── tailwind.config.js
└── vite.config.js```

## 📦 Installation & Setup

To run this project locally, follow these steps:

1. **Clone the repository:**

   ```sh
   git clone https://github.com/genta-bahana-nagari/inventory-system.git
   cd inventory-system
   ```

2. **Set environment:**

   ```sh
   cp .env.example .env
   ```

   You will see this configuration and adjust them with your database configuration:

   ```sh
    DB_CONNECTION=sqlite
    # DB_HOST=127.0.0.1
    # DB_PORT=3306
    # DB_DATABASE=laravel
    # DB_USERNAME=root
    # DB_PASSWORD=
   ```

3. **Install dependencies:**

   ```sh
   composer install
   ```

4. **Migration, Key Generate, and Storage Link:**

   ```sh
   php artisan migrate
   php artisan key:generate
   php artisan storage:link # because I use image field in the migrations.
   ```

5. **Run the development server:**

   ```sh
   npm run dev
   ```

6. Open http://localhost:8000 in your browser.

---

## 🚀 Deployment

To deploy the project, you can use VPS with one of these services:

- **Nginx:** you can configure this way:
   ```sh
    server {
        listen 80;
        listen [::]:80;
        server_name your_domain_or_ip;
        root /var/www/your_project_directory/public;
        index index.php index.html index.htm;

        # Security Headers
        add_header X-Frame-Options "SAMEORIGIN" always;
        add_header X-XSS-Protection "1; mode=block" always;
        add_header X-Content-Type-Options "nosniff" always;
        add_header Referrer-Policy "no-referrer-when-downgrade" always;
        add_header Content-Security-Policy "default-src 'self' http: https: data: blob;" always;

        # Gzip Compression
        gzip on;
        gzip_vary on;
        gzip_min_length 1024;
        gzip_proxied expired no-cache no-store private must-revalidate auth;
        gzip_types text/plain text/css text/xml text/javascript application/x-javascript application/xml+rss;

        # Handle Laravel Routes
        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }

        # PHP Processing
        location ~ \.php$ {
            fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
            include fastcgi_params;
            fastcgi_hide_header X-Powered-By;
        }

        # Static Files Caching
        location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
            expires 1y;
            add_header Cache-Control "public, immutable";
        }

        # Security: Deny access to hidden files
        location ~ /\. {
            deny all;
        }

        # Security: Deny access to sensitive files
        location ~ /(\.env|\.git|composer\.(json|lock)|package\.json) {
            deny all;
        }

        # Favicon and robots.txt
        location = /favicon.ico { access_log off; log_not_found off; }
        location = /robots.txt  { access_log off; log_not_found off; }
    }
   ```
- **Apache:** you can configure this way:
   ```sh
   <VirtualHost *:80>

        ServerAdmin admin@testapp.local
        ServerName testapp.local
        DocumentRoot /var/www/your_project_directory/public

        <Directory />
                Options FollowSymLinks
                AllowOverride None
        </Directory>
        <Directory /var/www/your_project_directory>
                AllowOverride All
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

    </VirtualHost>
   ```

---

## 👤 Author

- **Genta Bahana Nagari** – [LinkedIn](https://www.linkedin.com/in/genta-bahana-nagari/) | [GitHub](https://github.com/genta-bahana-nagari)

---

## 🌟 Show Your Support

If you find this script helpful, feel free to ⭐ the repository and share it with others!

---

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---
