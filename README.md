<p align="center">
  <img src="icon.png" width="120" alt="DigiAudit">
</p>

<h1 align="center">DigiAudit</h1>

<p align="center">
  A WordPress health check by <a href="https://digipacket.net">Digipacket</a>.<br>
  56 checks across security, performance, SEO and maintenance, explained in plain language.
</p>

<p align="center">
  <a href="https://github.com/digipacket-net/digiaudit/releases/latest/download/digiaudit.zip"><b>Download digiaudit.zip</b></a>
  ·
  <a href="https://github.com/digipacket-net/digiaudit/releases/latest">All releases</a>
  ·
  <a href="https://digipacket.net/contact">Support</a>
</p>

---

> **Interface language.** The plugin's admin screens, e-mails and printable report are in **French**.
> This documentation is in English.

## Contents

- [What it does](#what-it-does)
- [Requirements](#requirements)
- [Installation](#installation)
- [Running your first scan](#running-your-first-scan)
- [Reading the results](#reading-the-results)
- [Requesting a quote](#requesting-a-quote)
- [Settings](#settings)
- [History, report and dashboard widget](#history-report-and-dashboard-widget)
- [The 56 checks](#the-56-checks)
- [Privacy and data](#privacy-and-data)
- [Updating and uninstalling](#updating-and-uninstalling)
- [For agencies: white-label configuration](#for-agencies-white-label-configuration)
- [Webhook](#webhook)
- [Developer reference](#developer-reference)
- [FAQ](#faq)
- [Changelog](#changelog)
- [License](#license)

## What it does

DigiAudit scans a WordPress site from the inside and gives it a score out of 100. For every problem it finds, it tells
the site owner three things: **what was found**, **why it matters for their business**, and **how it gets fixed**.

When something needs fixing, the owner ticks the items they care about and sends a quote request to Digipacket in one
click.

- Overall score out of 100, a grade from A to E, and a score per category
- 56 checks: Security (23), Performance (11), SEO (14), Maintenance (8)
- Change since the previous scan
- One-click quote request with a reference number
- Optional weekly scan with e-mail alerts
- Printable report (save it as PDF from the browser)
- Dashboard widget and a red badge in the admin menu when critical issues are open

## Requirements

| | Minimum |
|---|---|
| WordPress | 5.8 |
| PHP | 7.4 |
| Permission | An account that can `manage_options` (administrators by default) |

The scan makes HTTP requests to the site itself (to check headers, HTTPS, exposed files and the home page). If the
server blocks loopback requests, the checks that depend on them report that they could not run instead of guessing.

## Installation

1. Download [`digiaudit.zip`](https://github.com/digipacket-net/digiaudit/releases/latest/download/digiaudit.zip)
   from the latest release. Do not unzip it.
2. In WordPress, go to **Plugins → Add New → Upload Plugin**.
3. Choose `digiaudit.zip`, click **Install Now**, then **Activate**.

After activation you are taken straight to the plugin's page. It is also in the admin menu under **Diagnostic**.

**Manual install:** unzip the archive and upload the `digiaudit` folder to `/wp-content/plugins/`, then activate it
from the **Plugins** screen.

## Running your first scan

1. Open **Diagnostic** in the admin menu.
2. Click **Lancer le diagnostic gratuit** (*Run the free scan*).
3. Keep the page open. A progress bar runs through the four categories one after the other; a scan usually takes
   between a few seconds and a minute, depending on the server.

The scan only reads. It does not change any setting, file or content on the site.

## Reading the results

### Score and grade

| Score | Grade | Health |
|---|---|---|
| 90–100 | A | Good |
| 80–89 | B | Good |
| 75–79 | B | Needs work |
| 60–74 | C | Needs work |
| 55–59 | D | Needs work |
| 40–54 | D | At risk |
| 0–39 | E | At risk |

Each check carries a weight. A passed check earns its full weight, a warning earns half, and a critical issue earns
nothing. The score is the share of points earned, so fixing a critical issue on a heavily weighted check moves the
score most. Checks that could not run are left out of the calculation. After the second scan, the page also shows how many points the score gained or lost since the previous one.

### Issue statuses

| Status | Meaning |
|---|---|
| **Critique** (critical) | A real risk to the site or the business. Fix it first. |
| **À améliorer** (warning) | Not urgent, but worth fixing. |
| **Conforme** (passed) | Nothing to do. |
| **Non vérifié** (not checked) | The check could not run on this server (for example, a blocked request). It is left out of the score. |

### Issue details

Click an issue to open it. It shows:

- **Ce que nous avons constaté** (*what we found*): what the scan actually saw, with details such as file names or
  plugin names.
- **Pourquoi c'est important** (*why it matters*): the consequence for the business, in plain language.
- **Solution recommandée** (*recommended fix*): what the fix involves, and its level: quick fix, standard job or
  advanced job.

Use the filter buttons above the list to show one category at a time. Passed checks and checks that could not run are
folded into two sections at the bottom of the page.

## Requesting a quote

1. Tick the issues you want fixed. A bar at the bottom of the page counts your selection.
2. Click **Demander un devis pour la sélection** (*Request a quote for the selection*), or **Demander un devis
   gratuit** (*Request a free quote*) in the card next to the score.
3. Fill in the form: name, company, e-mail, phone, how you prefer to be contacted (e-mail or phone), how urgent it
   is, and an optional message. E-mail and phone are pre-filled from your [contact details](#your-contact-details).
4. Tick the consent box and send.

You get a reference number (format `DA-YYMMDD-XXXX`) on screen and an acknowledgement by e-mail. Digipacket receives
the request with the selected issues, the other problems found, and the site's technical environment (WordPress, PHP,
theme and plugin versions).

Past requests are listed on the **Historique** (*History*) page.

## Settings

Open **Diagnostic → Réglages** (*Settings*).

### Automatic monitoring

| Setting | Default | What it does |
|---|---|---|
| **Analyse hebdomadaire** (*Weekly scan*) | On | Runs a scan once a week in the background, through WP-Cron. |
| **Alertes par e-mail** (*E-mail alerts*) | On | E-mails you when a weekly scan finds a new critical issue or the score drops. |
| **Adresse des alertes** (*Alert address*) | Site admin e-mail | Where those alerts go. |
| **Assistance proactive** (*Proactive support*) | Off | When a weekly scan finds a new critical issue, also sends the report to Digipacket automatically, so they can offer to fix it. Nothing is sent unless you turn this on. |

WP-Cron runs when the site receives visits. On a site with very little traffic, the weekly scan may run later than
expected.

### Your contact details

Tells Digipacket how to reach you about your site. Choose one:

- **Utiliser les coordonnées de mon site** (*Use my site's details*): the site's admin e-mail address.
- **Me contacter à d'autres coordonnées** (*Contact me elsewhere*): enter an e-mail address, a phone number, or both,
  plus an optional message (for example, the best time to call).

These details are included in proactive-support alerts and pre-fill the quote form.

## History, report and dashboard widget

- **Historique** (*History*): the last 30 scans with their scores, and the last 50 quote requests.
- **Printable report**: on the results page, click **Rapport PDF**. The report opens in a new tab; use your
  browser's **Print → Save as PDF**.
  The report carries the agency's name and contact details.
- **Dashboard widget**: the latest score and grade, the number of critical issues and warnings, and the date of the
  last scan, on the WordPress dashboard.
- **Menu badge**: the number of critical issues, shown in red next to **Diagnostic** in the admin menu.

## The 56 checks

### Security (23)

| Check | Looks at |
|---|---|
| WordPress version | Whether WordPress core is up to date |
| Plugin updates | Plugins with an available update |
| Theme updates | Themes with an available update |
| Abandoned or removed plugins | Plugins closed on WordPress.org, or not updated there for more than two years |
| Inactive plugins | Installed but deactivated plugins, still exploitable |
| Unused themes | Themes other than the active theme, its parent and one default fallback |
| Secure connection (HTTPS) | Whether the site and admin use HTTPS |
| SSL certificate | Validity and expiry date of the certificate |
| Mixed content | HTTP resources loaded on HTTPS pages |
| Debug mode | `WP_DEBUG` and error display on a live site |
| Exposed sensitive files | Backups, logs, `.env`, `.git` and similar files reachable from the web |
| Built-in file editor | Whether the theme/plugin editor is enabled |
| "admin" username | A user called `admin` |
| Administrator accounts | Number of administrators |
| WordPress security keys | Missing or default keys and salts |
| Database prefix | Default `wp_` table prefix |
| XML-RPC interface | Whether XML-RPC is enabled |
| User enumeration | Usernames exposed through author URLs or the REST API |
| Directory listing | Folders that list their contents |
| Visible WordPress version | Version number exposed in the page source |
| HTTP security headers | HSTS, X-Frame-Options, X-Content-Type-Options and similar headers |
| Firewall and login protection | A security plugin or brute-force protection |
| Configuration file permissions | Permissions on `wp-config.php` |

### Performance (11)

| Check | Looks at |
|---|---|
| PHP version | Whether the PHP branch still receives security fixes |
| Server response time | Time to first byte of the home page |
| Page cache | Whether pages are served from a cache |
| Persistent object cache | Redis, Memcached or similar |
| Page compression | Gzip or Brotli |
| Autoloaded data | Size of the options loaded on every page |
| Database clutter | Revisions, spam, trash and expired transients |
| Image weight | Very heavy images in the media library (over 500 KB by default) |
| Home page assets | Number of scripts and stylesheets loaded |
| Active plugins | Number of active plugins |
| Available memory | PHP memory limit |

### SEO (14)

| Check | Looks at |
|---|---|
| Visibility in Google | The "discourage search engines" setting |
| robots.txt | Presence and blocking rules |
| Page addresses (permalinks) | Readable URLs instead of `?p=123` |
| Site title and tagline | Default or empty values |
| SEO plugin | Yoast, Rank Math, SEOPress or similar |
| Home page title | Presence and length of `<title>` |
| Home page description | Presence and length of the meta description |
| Main heading (H1) | Exactly one H1 on the home page |
| XML sitemap | A sitemap that search engines can find |
| Image alt text | Images without alternative text |
| Mobile compatibility | Viewport meta tag |
| Social media preview | Open Graph tags |
| Structured data | Schema.org markup |
| Site icon (favicon) | Whether a site icon is set |

### Maintenance (8)

| Check | Looks at |
|---|---|
| Automatic backups | A known backup plugin, or a managed host that backs up automatically |
| Automatic security updates | Whether WordPress applies minor updates on its own |
| E-mail reliability | Whether e-mail goes through SMTP or a sending service |
| Recent technical errors | Recent PHP errors in `wp-content/debug.log` |
| Scheduled tasks | WP-Cron health and overdue tasks |
| Disk space | Free space on the server |
| Server modules | Required PHP extensions |
| Database version | MySQL / MariaDB version |

## Privacy and data

- **Nothing leaves the site without your action.** A quote is sent only when you submit the form and tick the consent
  box. Proactive support is off by default.
- **External calls during a scan:** only `api.wordpress.org`, to check the status of installed plugins. All other
  requests go to the site itself.
- **What a quote request contains:** your contact details and message, the selected issues, the other issues found,
  the score, and the site's technical environment (URL, WordPress and PHP versions, theme, plugin list).
- **Where data is stored:** in the site's own database, in the options `digipacket_audit_settings`,
  `digipacket_audit_last_scan`, `digipacket_audit_history` and `digipacket_audit_quotes`.

## Updating and uninstalling

**Update:** download the new `digiaudit.zip`, go to **Plugins → Add New → Upload Plugin** and upload it. WordPress
offers to replace the installed version. Your settings, history and quotes are kept.

**Uninstall:** deactivate the plugin, then click **Delete**. This removes every option, transient, scheduled task and
user preference the plugin created, on every site of a multisite network.

## For agencies: white-label configuration

The agency settings are not editable from the WordPress admin. They are read only from `config.php` at the root of the
plugin folder. Edit that file **before** you zip the plugin and install it on a client site.

| Key | Default | Purpose |
|---|---|---|
| `agency_name` | `Digipacket` | Name shown in the header, e-mails and report |
| `agency_email` | `dev@digipacket.net` | Address that receives quote requests and alerts |
| `agency_phone` | *(empty)* | Shown in the call to action, e-mails and report |
| `agency_website` | *(empty)* | Shown in e-mails and the report |
| `agency_logo` | *(empty)* | Absolute URL of a logo (PNG or SVG, about 200 × 60). Replaces the DigiAudit logo in the header |
| `support_url` | `https://digipacket.net/contact` | Target of the **Support** button. Empty hides the button |
| `primary_color` | `#2563eb` | Accent colour of the interface |
| `cta_title` | *(French text)* | Heading of the call-to-action card |
| `cta_text` | *(French text)* | Body of the call-to-action card |
| `response_delay` | `24 à 48 h ouvrées` | Response time promised to the client |
| `show_prices` | `false` | Show a "from" price on each issue and an overall estimate |
| `price_quick` | `49` | Starting price of a quick fix |
| `price_medium` | `149` | Starting price of a standard job |
| `price_complex` | `349` | Starting price of an advanced job |
| `currency` | `€` | Currency symbol |
| `webhook_url` | *(empty)* | URL that receives every quote request as JSON. See [Webhook](#webhook) |
| `webhook_secret` | *(empty)* | Secret used to sign webhook calls |

You can also override any of these values without editing the file, from a must-use plugin:

```php
add_filter( 'digipacket_audit_agency_config', function ( $config ) {
	$config['agency_email'] = 'quotes@example.com';
	return $config;
} );
```

> **E-mail deliverability depends on the client's server.** If the site has no SMTP set up, quote e-mails may never
> arrive. The "E-mail reliability" check flags this. To never lose a request, set a webhook as well.

## Webhook

When `webhook_url` is set, DigiAudit sends a `POST` request with a JSON body:

- on every quote request (event `quote.requested`);
- when proactive support is on and a weekly scan finds a new critical issue (event `scan.alert`).

### Headers

| Header | Value |
|---|---|
| `Content-Type` | `application/json; charset=utf-8` |
| `X-Digipacket-Audit-Event` | `quote.requested` or `scan.alert` |
| `X-Digipacket-Audit-Signature` | `sha256=<HMAC-SHA256 of the raw body>`, only when `webhook_secret` is set |

### Body

| Field | Content |
|---|---|
| `event` | Same as the event header |
| `quote` | Reference, client contact details, urgency, message, selected issue IDs |
| `site` | URL, site name, WordPress and PHP versions, theme, plugins |
| `score`, `grade` | Overall result |
| `counts` | Number of critical, warning and good results |
| `categories` | Score per category |
| `selected` | Issues the client selected |
| `issues` | Every issue found |
| `scanned_at` | Scan date (ISO 8601, UTC) |
| `plugin` | DigiAudit version |

### Verifying the signature

```php
$body     = file_get_contents( 'php://input' );
$expected = 'sha256=' . hash_hmac( 'sha256', $body, $secret );

if ( ! hash_equals( $expected, $_SERVER['HTTP_X_DIGIPACKET_AUDIT_SIGNATURE'] ?? '' ) ) {
	http_response_code( 401 );
	exit;
}
```

The webhook times out after 10 seconds. A 2xx response counts as delivered. A quote request fails only if both the
e-mail and the webhook fail.

## Developer reference

### Hooks

| Hook | Type | Use |
|---|---|---|
| `digipacket_audit_checks` | filter | Add or remove checks |
| `digipacket_audit_agency_config` | filter | Override `config.php` values |
| `digipacket_audit_capability` | filter | Capability needed to use the plugin (default `manage_options`) |
| `digipacket_audit_scan_results` | filter | Change results before the score is calculated |
| `digipacket_audit_quote_recipients` | filter | Add recipients to quote e-mails |
| `digipacket_audit_webhook_payload` | filter | Change the webhook body |
| `digipacket_audit_php_eol` | filter | End-of-support dates for PHP branches |
| `digipacket_audit_large_image_bytes` | filter | "Heavy image" threshold (default 500 KB) |
| `digipacket_audit_scan_completed` | action | Runs after every scan, with the scan array |
| `digipacket_audit_quote_sent` | action | Runs after every quote request, with the quote and scan arrays |

### Adding a check

Extend `Digipacket_Audit_Check`, describe it in `setup()`, return a result from `run()`, and register it with the
`digipacket_audit_checks` filter.

```php
class My_Check extends Digipacket_Audit_Check {

	protected function setup() {
		$this->id             = 'my_check';
		$this->category       = 'security'; // security | performance | seo | maintenance
		$this->title          = 'My check';
		$this->weight         = 5;          // Higher weight = bigger effect on the score.
		$this->effort         = 'quick';    // quick | medium | complex
		$this->risk           = 'Why this matters to the business.';
		$this->recommendation = 'What the fix involves.';
	}

	public function run( Digipacket_Audit_Context $ctx ) {
		$ok = true; // Your test here.

		return $ok
			? $this->good( 'Everything is fine.' )
			: $this->critical( 'Problem found.', array( 'detail line' ) );
	}
}

add_filter( 'digipacket_audit_checks', function ( $checks ) {
	$check                = new My_Check();
	$checks[ $check->id ] = $check;
	return $checks;
} );
```

### Naming

Classes `Digipacket_Audit_*`, constants `DIGIPACKET_AUDIT_*`, options, hooks and AJAX actions `digipacket_audit_*`,
CSS classes `dpa-`, text domain `digiaudit`.

## FAQ

**Does the scan slow down my site?**
No. It runs only when you start it, or once a week in the background. It does not add anything to the pages your
visitors see.

**Will it change anything on my site?**
No. Every check only reads. Fixes are done by Digipacket after you request a quote.

**A check says "Non vérifié" (not checked). Is that a problem?**
It means the check could not run on your server, usually because the server blocks requests to itself. It does not
lower your score.

**I requested a quote but Digipacket says they did not receive it.**
Your server probably cannot send e-mail. Check the "E-mail reliability" result, then [contact Digipacket](https://digipacket.net/contact)
directly with your reference number.

**Is the plugin available in English?**
Not yet. The interface is in French only.

**Can I use it on a multisite network?**
Yes. Each site has its own scans and settings.

## Changelog

### 1.0.0

- First public release.

## License

DigiAudit is free software released under the [GNU General Public License v2.0 or later](LICENSE.txt).

## Support

Questions or problems: [digipacket.net/contact](https://digipacket.net/contact).
