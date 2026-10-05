## Fork / Adaption (wolke.toschke.de)

Basiert auf dem AGPL-Projekt [Wacken2012/nextcloud-verein](https://github.com/Wacken2012/nextcloud-verein) (Branch/Tag develop bzw. v0.2.2-pre-release).
Angepasst für Nextcloud 35 und PHP 8.5 für https://wolke.toschke.de (Versionssuffix `-nc35`).

# 🤝 Nextcloud Vereins-App

Eine moderne, benutzerfreundliche **Nextcloud-App zur Verwaltung von Vereinen, Verbänden und Organisationen**. Mit vollständiger Mitglieder- und Finanzverwaltung.

**Status**: v0.2.2-pre ✅ **Released** | **Lizenz**: AGPL-3.0 | **Nextcloud**: 28+ | **Release**: 4. Dezember 2025

---

## Deutsch

### 📊 Release Status

| Version | Status | Release | Fokus |
|---------|--------|---------|-------|
| **v0.1.0-alpha** | ✅ Stabil | Nov 2025 | Basis CRUD, MVP |
| **v0.2.0-beta** | ✅ Released | 30. Nov 2025 | RBAC, Admin-Panel, CSV/PDF Export, Statistics |
| **v0.2.1** | ✅ Released | 1. Dez 2025 | API Docs, Developer Guide, Bundle-Optimierung |
| **v0.2.2-pre** | ✅ **Aktuell** | 4. Dez 2025 | Bugfixes, NC32-Kompatibilität, Privacy/Reminder Fixes |
| **v0.3.0** | 📋 Geplant | Q2 2026 | Kalender, Talk, Files, Deck Integration |
| **v1.0.0** | 🎯 Ziel | Q4 2026 | Production-Ready, App Store Release |

### 🆕 Was ist neu in v0.2.2-pre?

- **Bugfix-Release (NC32-kompatibel)**: ersetzt `ILogger` durch `Psr\Log\LoggerInterface`, liest Request-Bodies über `php://input`, fixt DI im `PrivacyService`, Syntax-Fix im `ReminderService`.
- **Stabile Export/Privacy/Reminder-APIs**: Endpunkte für Export/Consent/Policy/Reminder liefern keine 500er mehr; akzeptieren string|int IDs; ReminderLog verarbeitet Array- oder Objekt-Antworten.
- **Technische Verbesserungen**: Union Types für flexiblere Parameter, klarere Error-Responses, korrekte Service-Registrierung in `Application.php`.
- Details siehe `CHANGELOG.md` Abschnitt 0.2.2-pre.

### 🚧 Neu (develop, Ziel v0.3.0)

- Kalender mit RSVP: Events erstellen/ändern/löschen, RSVP (Ja/Nein/Vielleicht), eigene/pending RSVPs, Deadline & Teilnehmerlimit, Detail-Modal mit Antworten
- DSGVO-Verbesserungen: Consent-Typen, Audit-Log, Bulk-Consent, Löschprüfung, Policy speichern/abrufen, Export/Delete Endpunkte erweitert
- Automatische Erinnerungen: Hintergrund-Job, konfigurierbare E-Mail-Templates (Editor, Preview, Test-Mail), Reminder-Service/API
- Neue Admin-UI: Kalender-Frontend (Vue 3), E-Mail-Template-Editor, erweiterte Privacy-Settings

### Was kam in v0.2.0-beta?

✅ **Role-Based Access Control (RBAC)** — Vollständig implementiert
- Admin, Kassierer, Mitglied Rollen
- Granulare Berechtigungen für alle API-Endpoints (31 Methoden)
- Audit-Logging für Permission-Violations
- 20+ Unit Tests für RBAC-Systeme
- Permission Denial Tests bestanden ✅

✅ **Admin-Panel & Settings Integration** — Vollständig implementiert
- Native Nextcloud Settings Seite (Settings → Administration → Verein)
- Rollen-Management im Admin-Panel
- Permission-Verwaltung & Benutzer-Zuweisung
- IAppContainer Dependency Injection Integration

✅ **Datenvalidierung & Sicherheit** — Vollständig implementiert
- IBAN/BIC Validierung (ISO 13616 + SWIFT ISO 9362)
- E-Mail Format & MX-Check Validierung (RFC 5322)
- SEPA XML Schema Validierung (pain.001)
- Eingabe-Sanitization mit NFKC Unicode-Normalisierung
- 69+ Unit Tests für Validierung (100% Pass-Rate) ✅
- @RequirePermission Decorators auf allen kritischen Endpoints

✅ **CSV/PDF Export-Funktionalität** — Vollständig implementiert
- CSV Export mit UTF-8 BOM (Excel-kompatibel, Semikolon-Trenner)
- PDF Export mit TCPDF für professionelle Layouts
- 4 Export-Endpunkte (Members CSV/PDF, Fees CSV/PDF)
- RBAC-geschützt mit @RequirePermission Decorators
- 41 Tests für Export-Services & Controller (100% Pass-Rate) ✅
- CSV Endpoints: HTTP 200 OK (live & getestet) ✅
- Fehlerbehandlung für leere Datenbanken
- Sonderzeichen-Handling (Umlaute, Anführungszeichen) ✅

✅ **Dashboard-Statistiken** — Vollständig implementiert
- 4 Dashboard-Kacheln mit Live-Daten
- Mitgliederstatistiken (Anzahl, Rollen, Neuzugänge)
- Gebührenstatistiken (Betrag nach Status)
- Fällige Gebühren-Tracking (overdue detection)
- Vue.js 3 Frontend mit reaktiven Daten
- API-Integration mit `/statistics/members` & `/statistics/fees`

✅ **Verbesserte API Sicherheit** — Vollständig implementiert
- @RequirePermission Decorators auf 31 Controller-Methoden
- AuthorizationMiddleware mit automatischen Permission-Checks
- HTTP 403 Forbidden bei fehlenden Berechtigungen
- Konsistente Error-Response-Formate
- Input-Sanitization auf allen POST/PUT Endpoints

---

## ✨ Features — Deutsch

### 👥 Mitgliederverwaltung
- Mitglieder anlegen, bearbeiten, löschen (mit Validierung)
- Datenfelder: Name, E-Mail, Adresse, IBAN, BIC, Rolle
- Rollen: Mitglied, Kassierer, Admin (mit rollenbasierten Berechtigungen)
- Responsive Tabelle mit Inline-Editing
- Duplikat-Prüfung für IBAN/E-Mail
- Datum-Tracking: Beitrittsdatum, Änderungsdatum

### 💰 Finanzverwaltung
- Gebühren und Beitragsverfolgung
- Status-Tracking: offen, bezahlt, überfällig
- Statistiken: Gesamtausstände, bezahlte Beträge, Trends
- CSV/PDF Export für Jahresabschlüsse
- Schnelle Übersicht aller Transaktionen
- Filterung nach Zeitraum & Mitglied

### 📊 Datenexport
- **CSV Export**: UTF-8 BOM, Semikolon-Separator (Excel-kompatibel)
  - Mitgliederliste exportieren
  - Gebührenübersicht exportieren
- **PDF Export**: Professionelle Layouts mit TCPDF
  - Gebührenlisten mit Tabellen
  - Mitgliederlisten mit Formatierung
  - Prädefinierte Kopf- und Fußzeilen
- Beide Formate RBAC-geschützt

### 🎨 User Experience
- Dark Mode Support
- Responsive Design (Desktop, Tablet, Mobile)
- Nextcloud-native Authentifizierung & Session-Management
- Schnelle Vue 3 + Vite Frontend (SPA)
- Konforme Nextcloud Design-Variablen

### 🔐 Sicherheit & Berechtigungen
- Role-Based Access Control (RBAC) mit Admin/Kassierer/Mitglied Rollen
- Granulare Permission-Verwaltung für alle Endpoints
- Audit-Logging für Permission-Violations
- Input-Validierung & Sanitization (IBAN, BIC, Email, SEPA XML)
- CSRF-Schutz durch Nextcloud AppFramework

---

## English

### 📊 Release Status

| Version | Status | Release | Focus |
|---------|--------|---------|-------|
| **v0.1.0-alpha** | ✅ Stable | Nov 2025 | Basic CRUD, MVP |
| **v0.2.0-beta** | ✅ Released | Nov 30, 2025 | RBAC, Admin Panel, CSV/PDF Export, Statistics |
| **v0.2.1** | ✅ Released | Dec 1, 2025 | API Docs, Developer Guide, Bundle Optimization |
| **v0.2.2-pre** | ✅ **Current** | Dec 4, 2025 | Bug fixes, NC32 compatibility, privacy/reminder fixes |
| **v0.3.0** | 📋 Planned | Q2 2026 | Calendar, Talk, Files, Deck Integration |
| **v1.0.0** | 🎯 Goal | Q4 2026 | Production-Ready, App Store Release |

### 🆕 What's New in v0.2.2-pre?

- **Bugfix release (NC32 compatible)**: replaced `ILogger` with `Psr\Log\LoggerInterface`, reads request bodies via `php://input`, DI fix in `PrivacyService`, syntax fix in `ReminderService`.
- **Stable export/privacy/reminder APIs**: export/consent/policy/reminder endpoints no longer 500; accept string|int IDs; ReminderLog handles array or object responses.
- **Technical improvements**: union types for flexible parameters, clearer error responses, proper service registration in `Application.php`.
- See `CHANGELOG.md` 0.2.2-pre for full details.

### 🚧 New (develop, target v0.3.0)

- Calendar with RSVP: create/update/delete events, RSVP (yes/no/maybe), my/pending RSVPs, deadline & capacity limits, detail modal with responses
- GDPR upgrades: consent types, audit log, bulk consent, delete-check endpoint, save/fetch policy, extended export/delete endpoints
- Automatic reminders: background job, configurable email templates (editor, preview, test mail), reminder service/API
- New admin UI: calendar frontend (Vue 3), email template editor, extended privacy settings

### What came in v0.2.0-beta?

✅ **Role-Based Access Control (RBAC)** — Fully Implemented
- Admin, Treasurer, Member roles
- Granular permissions for all API endpoints (31 methods)
- Audit logging for permission violations
- 20+ unit tests for RBAC systems
- Permission denial tests passed ✅

✅ **Admin Panel & Settings Integration** — Fully Implemented
- Native Nextcloud settings page (Settings → Administration → Verein)
- Role management in admin panel
- Permission management & user assignment
- IAppContainer dependency injection integration

✅ **Data Validation & Security** — Fully Implemented
- IBAN/BIC validation (ISO 13616 + SWIFT ISO 9362)
- Email format & MX-check validation (RFC 5322)
- SEPA XML schema validation (pain.001)
- Input sanitization with NFKC Unicode normalization
- 69+ unit tests for validation (100% pass rate) ✅
- @RequirePermission decorators on all critical endpoints

✅ **CSV/PDF Export Functionality** — Fully Implemented
- CSV export with UTF-8 BOM (Excel-compatible, semicolon separator)
- PDF export with TCPDF for professional layouts
- 4 export endpoints (Members CSV/PDF, Fees CSV/PDF)
- RBAC-protected with @RequirePermission decorators
- 41 tests for export services & controllers (100% pass rate) ✅
- CSV endpoints: HTTP 200 OK (live & tested) ✅
- Error handling for empty databases

✅ **Enhanced API Security** — Fully Implemented
- @RequirePermission decorators on 31 controller methods
- AuthorizationMiddleware with automatic permission checks
- HTTP 403 Forbidden for missing permissions
- Consistent error response formats
- Input sanitization on all POST/PUT endpoints

---

## ✨ Features — English

### 👥 Member Management
- Create, edit, delete members (with validation)
- Data fields: Name, Email, Address, IBAN, BIC, Role
- Roles: Member, Treasurer, Admin (with role-based permissions)
- Responsive table with inline editing
- Duplicate checking for IBAN/Email
- Date tracking: joining date, last modified

### 💰 Finance Management
- Fee and contribution tracking
- Status tracking: pending, paid, overdue
- Statistics: total outstanding, paid amounts, trends
- CSV/PDF export for financial reports
- Quick overview of all transactions
- Filtering by date range & member

### 📊 Data Export
- **CSV Export**: UTF-8 BOM, semicolon separator (Excel-compatible)
  - Export member list
  - Export fees overview
- **PDF Export**: Professional layouts with TCPDF
  - Fee lists with tables
  - Member lists with formatting
  - Predefined headers and footers
- Both formats RBAC-protected

### 🎨 User Experience
- Dark mode support
- Responsive design (desktop, tablet, mobile)
- Nextcloud-native authentication & session management
- Fast Vue 3 + Vite frontend (SPA)
- Compliant with Nextcloud design variables

### 🔐 Security & Permissions
- Role-Based Access Control (RBAC) with Admin/Treasurer/Member roles
- Granular permission management for all endpoints
- Audit logging for permission violations
- Input validation & sanitization (IBAN, BIC, Email, SEPA XML)
- CSRF protection through Nextcloud AppFramework

---

## 🚀 Installation — Deutsch

### Anforderungen
- **Nextcloud**: 28.0 oder höher
- **PHP**: 8.1 oder höher
- **Database**: MySQL/MariaDB oder PostgreSQL
- **Disk Space**: ~10 MB

### Quick Install

```bash
# 1. Repo klonen
cd /var/www/nextcloud/apps/
git clone https://github.com/yourusername/nextcloud-verein.git verein
cd verein

# 2. Dependencies installieren
npm install
npm run build

# 3. App aktivieren
sudo -u www-data php /var/www/nextcloud/occ app:enable verein

# 4. Admin-Rollen konfigurieren
# In Nextcloud: Settings → Administration → Verein (Tab)
# Benutzer Rollen zuweisen: Admin, Kassierer, Mitglied

# Fertig! App ist einsatzbereit
```

**Detaillierte Anleitung**: Siehe [INSTALLATION.md](./INSTALLATION.md)

---

## 🚀 Installation — English

### Requirements
- **Nextcloud**: 28.0 or higher
- **PHP**: 8.1 or higher
- **Database**: MySQL/MariaDB or PostgreSQL
- **Disk Space**: ~10 MB

### Quick Install

```bash
# 1. Clone repository
cd /var/www/nextcloud/apps/
git clone https://github.com/yourusername/nextcloud-verein.git verein
cd verein

# 2. Install dependencies
npm install
npm run build

# 3. Enable app
sudo -u www-data php /var/www/nextcloud/occ app:enable verein

# 4. Configure admin roles
# In Nextcloud: Settings → Administration → Verein (tab)
# Assign user roles: Admin, Treasurer, Member

# Done! App is ready to use
```

**Detailed guide**: See [INSTALLATION.md](./INSTALLATION.md)

---

## 🎯 Roadmap — Deutsch

### v0.1.0-alpha ✅ (Stable)
- ✅ Basic member management (CRUD)
- ✅ Fee management (CRUD)
- ✅ Responsive UI with dark mode
- ✅ Nextcloud integration

### v0.2.0-beta ✅ (Released Nov 30, 2025)
- ✅ Roles & permissions (RBAC)
- ✅ Admin panel & settings
- ✅ Data validation (IBAN, BIC, Email)
- ✅ CSV/PDF export
- ✅ 130+ unit tests (100% pass rate)

### v0.2.1 ✅ (Released Dec 1, 2025)
- ✅ API Documentation (OpenAPI 3.0)
- ✅ Developer Guide (Bilingual)
- ✅ Bundle optimization (40% reduction)
- ✅ PDF export fully functional
- ✅ Bilingual documentation (DE/EN)

### v0.3.0 📋 (Planned Q2 2026)
- Kalender mit RSVP, Deadlines, Teilnehmerlimit
- Erinnerungen & E-Mail-Templates
- Datenschutz: Consents, Audit-Log, Löschprüfung
- Talk/Files/Deck Integrationen (Plan)
- DSGVO-Compliance (Art. 6-34)

### v1.0.0 🎯 (Goal Q4 2026)
- Full stability & 100% test coverage
- SEPA XML export for bank transfers
- Comprehensive documentation & API documentation
- Internationalization (i18n)
- App Store release

---

## 🎯 Roadmap — English

### v0.1.0-alpha ✅ (Stable)
- ✅ Basic member management (CRUD)
- ✅ Fee management (CRUD)
- ✅ Responsive UI with dark mode
- ✅ Nextcloud integration

### v0.2.0-beta ✅ (Released Nov 30, 2025)
- ✅ Roles & permissions (RBAC)
- ✅ Admin panel & settings
- ✅ Data validation (IBAN, BIC, Email)
- ✅ CSV/PDF export
- ✅ 130+ unit tests (100% pass rate)

### v0.2.1 ✅ (Released Dec 1, 2025)
- ✅ API Documentation (OpenAPI 3.0)
- ✅ Developer Guide (Bilingual)
- ✅ Bundle optimization (40% reduction)
- ✅ PDF export fully functional
- ✅ Bilingual documentation (DE/EN)

### v0.3.0 📋 (Planned Q2 2026)
- Calendar with RSVP, deadlines, capacity
- Reminders & email templates
- Privacy: consents, audit log, delete checks
- Talk/Files/Deck integrations (planned)
- GDPR/DSGVO compliance (Art. 6-34)

### v1.0.0 🎯 (Goal Q4 2026)
- Full stability & 100% test coverage
- SEPA XML export for bank transfers
- Comprehensive documentation & API documentation
- Internationalization (i18n)
- App Store release

## 🎯 Roadmap — English

### v0.1.0-alpha ✅ (Current)
- ✅ Basic member management (CRUD)
- ✅ Fee management (CRUD)
- ✅ Responsive UI with dark mode
- ✅ Nextcloud integration

### v0.2.0-beta ✅ (100% complete, Released Dec 1, 2025)
- ✅ Roles & Permissions (RBAC)
- ✅ Admin Panel & Settings
- ✅ Data validation (IBAN, BIC, Email)
- ✅ CSV/PDF Export
- ✅ 130+ Unit Tests (100% pass rate)

### v0.2.1 📋 (Q1 2026)
- PDF export functionality (TCPDF fix)
- Bug fixes & performance optimization
- Enhanced error handling

### v0.3.0 📋 (Q2 2026)
- Calendar with RSVP, deadlines, capacity
- Automated reminders (cronjob) & email templates
- Privacy: consents, audit log, delete checks
- Notification system (email/talk) — planned

### v1.0.0 🎯 (Q4 2026, Production)
- Full stability & 100% test coverage
- SEPA XML export for bank transfers
- Comprehensive documentation & API docs
- Internationalization (i18n)

---

## 🛠️ Entwicklung — Deutsch

### Lokal entwickeln

```bash
# 1. Repository klonen
git clone <repo-url>
cd nextcloud-verein

# 2. Dependencies
npm install

# 3. Watch Mode (Vite Auto-Rebuild)
npm run dev

# 4. Produktion Build
npm run build

# 5. Zum Server synchen
./scripts/deploy-to-nextcloud.sh
```

### Projekt-Struktur

```
nextcloud-verein/
├── appinfo/
│   ├── info.xml              # App-Metadaten
│   └── routes.php            # API Routes
├── lib/
│   ├── Controller/           # PHP Controller (31 Methoden)
│   ├── Service/              # Business Logic (Validator, Exporter)
│   ├── Db/                   # Entity Models (Member, Fee)
│   ├── Middleware/           # AuthorizationMiddleware
│   ├── Attribute/            # RequirePermission Decorator
│   └── Rules/                # Validation Rules
├── js/
│   ├── components/           # Vue 3 Components
│   ├── api.js                # Axios API Wrapper
│   ├── main.js               # Entry Point
│   └── style.css             # Global Styles
├── tests/
│   ├── Unit/                 # PHP Unit Tests (RBAC, Validation)
│   ├── Integration/          # Export & Controller Tests
│   └── Feature/              # End-to-End Tests
├── templates/
│   └── main.php              # Main Nextcloud Template
├── scripts/
│   └── deploy-to-nextcloud.sh # Deployment Script
└── package.json
```

### Test ausführen

```bash
# PHP Unit Tests
./vendor/bin/phpunit

# Vue Components Tests (mit Vitest)
npm run test

# End-to-End Tests
npm run test:e2e
```

**Status**: 130+ Tests, 100% Pass-Rate ✅

---

## 🛠️ Development — English

### Local Development

```bash
# 1. Clone repository
git clone <repo-url>
cd nextcloud-verein

# 2. Dependencies
npm install

# 3. Watch mode (Vite auto-rebuild)
npm run dev

# 4. Production build
npm run build

# 5. Deploy to server
./scripts/deploy-to-nextcloud.sh
```

### Project Structure

```
nextcloud-verein/
├── appinfo/
│   ├── info.xml              # App metadata
│   └── routes.php            # API routes
├── lib/
│   ├── Controller/           # PHP controllers (31 methods)
│   ├── Service/              # Business logic (Validator, Exporter)
│   ├── Db/                   # Entity models (Member, Fee)
│   ├── Middleware/           # AuthorizationMiddleware
│   ├── Attribute/            # RequirePermission decorator
│   └── Rules/                # Validation rules
├── js/
│   ├── components/           # Vue 3 components
│   ├── api.js                # Axios API wrapper
│   ├── main.js               # Entry point
│   └── style.css             # Global styles
├── tests/
│   ├── Unit/                 # PHP unit tests (RBAC, Validation)
│   ├── Integration/          # Export & controller tests
│   └── Feature/              # End-to-end tests
├── templates/
│   └── main.php              # Main Nextcloud template
├── scripts/
│   └── deploy-to-nextcloud.sh # Deployment script
└── package.json
```

### Run Tests

```bash
# PHP unit tests
./vendor/bin/phpunit

# Vue component tests (with Vitest)
npm run test

# End-to-end tests
npm run test:e2e
```

**Status**: 130+ tests, 100% pass rate ✅

---

## 🤝 Contributing — Deutsch

Contributions sind sehr willkommen! Bitte beachte folgende Schritte:

1. **Fork** das Repository
2. **Branch erstellen**: `git checkout -b feature/your-feature`
3. **Tests schreiben** für neue Features
4. **Commit mit Nachricht**: `git commit -m 'feat: add your feature'`
5. **Push**: `git push origin feature/your-feature`
6. **Pull Request** öffnen mit Beschreibung

**Guidelines**: Siehe [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## 🤝 Contributing — English

Contributions are very welcome! Please follow these steps:

1. **Fork** the repository
2. **Create branch**: `git checkout -b feature/your-feature`
3. **Write tests** for new features
4. **Commit with message**: `git commit -m 'feat: add your feature'`
5. **Push**: `git push origin feature/your-feature`
6. **Open pull request** with description

**Guidelines**: See [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## 🐛 Known Issues & Limitations — Deutsch

### v0.2.0-beta Status
- ✅ RBAC & Berechtigungen — IMPLEMENTIERT
- ✅ Datenvalidierung — IMPLEMENTIERT  
- ✅ CSV Export — HTTP 200 OK (getestet)
- 🟡 PDF Export — Code fertig, TCPDF Dependency-Issue in Nextcloud Runtime (akzeptabel für Beta)
- ✅ Admin-Panel — IMPLEMENTIERT
- ✅ 130+ Tests — 100% Pass-Rate

### Bekannte Einschränkungen
- PDF Export blockiert durch TCPDF-Klassenladen in Nextcloud AppFramework
  - Workaround: CSV Export verwenden oder direkte PHP-Aufrufe
  - Zielversion für Fix: v0.2.1 oder v0.3.0
- SEPA XML Export geplant für v0.3.0
- Event/Kalender-Integration geplant für v0.3.0

---

## 🐛 Known Issues & Limitations — English

### v0.2.0-beta Status
- ✅ RBAC & Permissions — IMPLEMENTED
- ✅ Data Validation — IMPLEMENTED
- ✅ CSV Export — HTTP 200 OK (tested)
- 🟡 PDF Export — Code complete, TCPDF dependency issue in Nextcloud runtime (acceptable for beta)
- ✅ Admin Panel — IMPLEMENTED
- ✅ 130+ Tests — 100% pass rate

### Known Limitations
- PDF export blocked by TCPDF class loading in Nextcloud AppFramework
  - Workaround: Use CSV export or direct PHP calls
  - Target version for fix: v0.2.1 or v0.3.0
- SEPA XML export planned for v0.3.0
- Event/calendar integration planned for v0.3.0

---

## 📝 Lizenz / License

**AGPL-3.0** — Siehe [LICENSE](./LICENSE) für Details.

Diese App muss unter der gleichen Lizenz verteilt werden und ist für die Verwendung in Nextcloud-Instanzen konzipiert.

---

## ❓ Support — Deutsch & English

- **GitHub Issues** (Deutsch/English): [Bugs & Feature Requests](https://github.com/Wacken2012/nextcloud-verein/issues)
- **Discussions** (Deutsch/English): [Q&A & Ideas](https://github.com/Wacken2012/nextcloud-verein/discussions)

---

## 📖 Dokumentation

| Dokument | Beschreibung |
|----------|--------------|
| [API Documentation](docs/api/README.md) | REST API Referenz mit Beispielen |
| [OpenAPI Spec](docs/api/openapi.yaml) | OpenAPI 3.0 Spezifikation (Swagger) |
| [Developer Guide](docs/DEVELOPER_GUIDE.md) | Setup, Architektur, Contributing |
| [Contributing](CONTRIBUTING.md) | Richtlinien für Beiträge |
| [Roadmap](ROADMAP.md) | Geplante Features & Versionen |
| [Installation](INSTALLATION.md) | Installationsanleitung |

---

## 📚 Tech Stack

**Frontend**:
- Vue 3 (Composition API)
- Vite (Bundler)
- Axios (HTTP Client)
- CSS3 (Responsive Design)

**Backend**:
- PHP 8.1+
- Nextcloud AppFramework
- Doctrine ORM
- PHPUnit (Testing)

**Database**:
- MySQL/MariaDB
- PostgreSQL
- SQLite (Development)

**Additional Libraries**:
- TCPDF (PDF Generation)
- Symfony/Validator (IBAN/Email Validation)
- EasyOCR (Optional)

---

## 🙏 Danksagungen / Acknowledgments

Entwickelt mit ❤️ für Vereine und Organisationen, die ihre Verwaltung modernisieren möchten.

Inspiriert von [Nextcloud](https://nextcloud.com), [Vue.js](https://vuejs.org) und der Open-Source Community!

**Special Thanks** to:
- [Nextcloud Community](https://nextcloud.com/community/)
- [Vuejs Community](https://vuejs.org)
- All contributors and testers

---

## 📋 V0.2.0-Beta Features Summary

### Implemented ✅
| Feature | Status | Tests | Notes |
|---------|--------|-------|-------|
| Member Management (CRUD) | ✅ | 25+ | Full IBAN/BIC validation |
| Fee Management (CRUD) | ✅ | 20+ | Status tracking, statistics |
| RBAC & Permissions | ✅ | 20+ | Admin/Treasurer/Member roles |
| Admin Panel | ✅ | - | Native Nextcloud integration |
| CSV Export | ✅ | 15+ | UTF-8 BOM, live tested |
| PDF Export | ✅ Code | 13+ | TCPDF dependency issue |
| Input Validation | ✅ | 69+ | IBAN/BIC/Email/SEPA |
| Authentication | ✅ | - | Nextcloud native |
| Dark Mode | ✅ | - | Full CSS support |
| Responsive UI | ✅ | - | Mobile/tablet ready |

**Total**: 130+ tests, 350+ assertions, 100% pass rate ✅

---

**Bereit zum Starten?** → [Installation Guide](./INSTALLATION.md) | [Roadmap](./ROADMAP.md)

**Ready to get started?** → [Installation Guide](./INSTALLATION.md) | [Roadmap](./ROADMAP.md)

---

**Nextcloud Vereins-App v0.2.0-beta** | Made with ❤️ | [GitHub](https://github.com/yourusername/nextcloud-verein) | [License: AGPL-3.0](./LICENSE)
