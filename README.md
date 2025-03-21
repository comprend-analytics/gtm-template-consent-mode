# Google Tag Manager - Tag Template - Consent Mode

<br>

## 📖 Features Overview

<br>

|**Feature**                                   | **Description**                                |
|:--------------------------------------------:|------------------------------------------------|
| **Default&nbsp;Consent**                     | Set default consent state.                     |
| **Update&nbsp;Consent**                      | Set updated consent state.                     |
| **Region-Specific&nbsp;Behavior**            | Configure different consent state based on regions. Automatically include EEA regions for localized privacy requirements.|
| **Manage&nbsp;Consent&nbsp;Types**           | Configure each consent type individually or read them from a variable. Consent types include **analytics_storage**, **ad_storage**, **ad_user_data**, **ad_personalization**, and optional types like **personalization_storage**, **functionality_storage**, and **security_storage**.|
| **Consent&nbsp;Integrations**  | Out-of-the-box integrations with Microsoft Clarity, Microsoft Advertising (UET), and Microsoft Invest (Xandr). Automatically reads relevant consent states (**analytics_storage** or **ad_storage**) to ensure compliance.|
| **URL&nbsp;Passthrough**                     | When consent is denied, URL passthrough preserves necessary analytics/ad information in URL parameters.|
| **Ads&nbsp;Data&nbsp;Redaction**             | Ads data redaction additionally anonymizes ad-click identifiers if **ad_storage** is denied.|
| **Data&nbsp;Layer&nbsp;Events**              | Push events to the `dataLayer` whenever consent is set or updated. Supports predefined event names (`consent_default`, `consent_update`). Optionally provide a custom event name. Optionally include the **previous** consent state in data layer pushes for better tracking and debugging.|
| **Wait&nbsp;For&nbsp;Update**                | Delay queued tags (when using the **default** command) by a specified time, allowing asynchronous consent management platforms (CMP) to update the consent state before tags fire.|

<br>

## 📦 Installation

1. Download the template file `template.tpl` from this repository.
2. Go to your GTM workspace → **Templates**.
3. Click the **New**-button under **Tag Templates**.
4. **Import** the `template.tpl` file.

## ⚙️ Configuration

### Consent Command

- **default**: Set initial consent state on page load.
- **update**: Update existing consent states based on user interactions.

### Region Specific Behavior

- Provide [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) region codes to customize consent rules (e.g., `SE,DK,DE`).
- Automatically include EEA regions (optional).

### Consent Settings

- #### **Read Settings from Variable**:
  - Provide an object via a GTM variable that specifies consent states.
  - Valid values include:
    - Granted: `"granted"`, `"true"`, or boolean `true`.
    - Denied: `"denied"`, `"false"`, or boolean `false`.
    - Other values are considered as "(not set)" and ignored.

  _Example:_

  ```javascript
  {
    analytics_storage: "granted",
    ad_user_data: "denied",
    ad_personalization: true,
    personalization_storage: false
  }
  ```

- #### **Set Individual Consent Types**:
  - Configure each consent type individually from the GTM UI.
  - Optionally map a variable value to individual consent types.
  - Consent types:
    - `analytics_storage` (default: denied)
    - `ad_storage` (default: denied)
    - `ad_user_data` (default: denied)
    - `ad_personalization` (default: denied)
    - Additional optional types:
      - `personalization_storage` (default: not set)
      - `functionality_storage` (default: not set)
      - `security_storage` (default: not set)

<br>

### Additional Settings

#### Wait for Update (default command only)
- Delay firing queued Google tags to wait for consent updates.
- Specify the delay time in milliseconds (default: 500ms).

#### URL Passthrough
- Preserve analytics/ad information via URL parameters if consent is denied.

#### Ads Data Redaction
- Further anonymize ad data when `ad_storage` consent is denied.

#### Data Layer Event
- Trigger a data layer event (`consent_default`, `consent_update`, or custom event name) upon consent state changes.
- Optionally include previous consent states in the event payload.

#### Third-party Consent Integrations
> [!IMPORTANT]
> Consent integrations don't support region-specific consent settings.

Individually enable built-in consent integrations for:
- **Microsoft Clarity** (reads `analytics_storage`)
- **Microsoft Advertising (UET)** (reads `ad_storage`)
- **Microsoft Invest (Xandr)** (reads `ad_storage`)

<br>

## 🔗 Useful Documentation Links

- [Google Tag Manager - Consent Mode APIs](https://developers.google.com/tag-platform/tag-manager/templates/api#setdefaultconsentstate)
- [Google Consent Mode Overview](https://developers.google.com/tag-platform/security/concepts/consent-mode#consent-types)
- [Consent Mode - URL Passthrough](https://developers.google.com/tag-platform/security/guides/consent?consentmode=advanced#passthroughs)
- [Consent Mode & CMP Integration Guide](https://developers.google.com/tag-platform/security/guides/consent?consentmode=advanced#integrate_with_asynchronous_consent_management_platforms)
- [Microsoft Clarity Consent Mode Integration](https://learn.microsoft.com/en-us/clarity/setup-and-installation/cookie-consent)
- [Microsoft Advertising Consent Mode Integration](https://help.ads.microsoft.com/apex/index/3/en/60119)
- [Microsoft Invest Consent Mode Integration](https://learn.microsoft.com/en-us/xandr/invest/set-up-consent-mode-in-universal-pixel)

<br>

### 🌐 License

This GTM template is provided as-is under an open-source license for free use and modification.
