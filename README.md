# service-desk
Truist IT service-desk
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IT Service Desk Template Generator</title>
    <style>
        :root {
            --primary: #2b579a;
            --primary-dark: #1e3d6b;
            --bg: #f4f6f9;
            --card-bg: #ffffff;
            --text: #333333;
            --border: #cccccc;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 1100px;
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: var(--primary);
            margin-bottom: 5px;
        }
        .author {
            text-align: center;
            font-style: italic;
            color: #666;
            margin-bottom: 30px;
        }
        .grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        @media (max-width: 768px) {
            .grid { grid-template-columns: 1fr; }
        }
        .card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .card h2 {
            border-bottom: 2px solid var(--primary);
            padding-bottom: 8px;
            color: var(--primary);
            margin-top: 0;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            font-weight: 600;
            margin-bottom: 5px;
        }
        input, select, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid var(--border);
            border-radius: 4px;
            box-sizing: border-box;
            font-family: inherit;
        }
        textarea {
            resize: vertical;
        }
        .info-box {
            background-color: #e7f0fd;
            border-left: 4px solid var(--primary);
            padding: 10px;
            margin-bottom: 15px;
            font-size: 0.9em;
        }
        .btn {
            background-color: var(--primary);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            width: 100%;
            margin-bottom: 10px;
            transition: background 0.2s;
        }
        .btn:hover { background-color: var(--primary-dark); }
        .btn-secondary {
            background-color: #28a745;
        }
        .btn-secondary:hover { background-color: #218838; }
        #outputTemplate {
            background: #f8f9fa;
            border: 1px solid #ddd;
            font-family: 'Courier New', Courier, monospace;
            height: 380px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>IT Service Desk Template Generator</h1>
    <div class="author">by Sandip Payghan</div>

    <div class="grid">
        <!-- LEFT PANEL: Inputs -->
        <div class="card">
            <h2>1. Teammate & Device Details</h2>
            <div class="grid" style="grid-template-columns: 1fr 1fr; gap: 10px;">
                <div class="form-group">
                    <label for="userId">User ID</label>
                    <input type="text" id="userId" placeholder="e.g., t123456">
                </div>
                <div class="form-group">
                    <label for="userName">User Name</label>
                    <input type="text" id="userName" placeholder="e.g., John Doe">
                </div>
            </div>

            <div class="grid" style="grid-template-columns: 1fr 1fr; gap: 10px;">
                <div class="form-group">
                    <label for="callbackNum">Call Back Number</label>
                    <input type="text" id="callbackNum" placeholder="e.g., 555-0199">
                </div>
                <div class="form-group">
                    <label for="shiftTime">Shift Time</label>
                    <input type="text" id="shiftTime" placeholder="e.g., 08:00 - 17:00">
                </div>
            </div>

            <div class="form-group">
                <label for="workLocation">Work Location</label>
                <select id="workLocation">
                    <option value="Office">Office</option>
                    <option value="Branch">Branch</option>
                    <option value="Remote">Remote</option>
                    <option value="Contact Center">Contact Center</option>
                </select>
            </div>

            <div class="grid" style="grid-template-columns: 1fr 1fr; gap: 10px;">
                <div class="form-group">
                    <label for="deviceType">Device Type</label>
                    <select id="deviceType">
                        <option value="Prod VDI">Prod VDI</option>
                        <option value="Dev VDI">Dev VDI</option>
                        <option value="Branch VDI">Branch VDI</option>
                        <option value="Laptop">Laptop</option>
                        <option value="Desktop">Desktop</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="wsid">Workstation ID (WSID)</label>
                    <input type="text" id="wsid" placeholder="e.g., WS12345">
                </div>
            </div>

            <h2>2. Application & Issue</h2>
            <div class="form-group">
                <label for="targetApp">Target Application</label>
                <select id="targetApp" onchange="populateIssues()">
                    <option value="">-- Select Application --</option>
                    <option value="Adobe Acrobat">Adobe Acrobat (Reader / Pro)</option>
                    <option value="Enterprise Teller">Enterprise Teller</option>
                    <option value="Microsoft Outlook">Microsoft Outlook</option>
                    <option value="Microsoft Teams">Microsoft Teams</option>
                    <option value="Virtual Desktop (VDI)">Virtual Desktop (VDI)</option>
                </select>
            </div>

            <div class="form-group">
                <label for="issueError">Issue / Error</label>
                <select id="issueError" onchange="populateIssueDetails()">
                    <option value="">-- Select Error/Issue --</option>
                </select>
            </div>
        </div>

        <!-- RIGHT PANEL: Actions -->
        <div class="card">
            <h2>3. Application Context</h2>
            <div class="form-group">
                <label for="shortDesc">Short Description</label>
                <input type="text" id="shortDesc">
            </div>

            <div class="form-group">
                <label for="tsSteps">Troubleshooting Steps performed</label>
                <textarea id="tsSteps" rows="8"></textarea>
            </div>

            <div class="info-box">
                <strong>Escalation Path (Internal Reference Only):</strong>
                <div id="escalationText">Select an application and issue to see escalation path.</div>
            </div>

            <button class="btn" onclick="generateTemplate()">Generate Automatic Template</button>
            <button class="btn btn-secondary" onclick="saveToCDrive()">Save Template to C Drive (sandip.txt)</button>
        </div>
    </div>

    <!-- PREVIEW BOX -->
    <div class="card" style="margin-top: 20px;">
        <h2>4. Generated Template Preview (Editable)</h2>
        <textarea id="outputTemplate" placeholder="Your generated ticket template will appear here..."></textarea>
    </div>
</div>

<script>
// Verbatim raw steps extracted from all in one.txt without modifying formatting or text
const knowledgeBase = {
    "Adobe Acrobat": [
        {
            error: '"Acrobat Trial: You can try this product for # days"',
            short: 'Adobe Acrobat (Reader / Pro) - error - "Acrobat Trial: You can try this product for # days"',
            steps: `End all Acrobat processes from Task Manager and relaunch application\nVerify AD group (L-SW-U-Adobe-AcrobatProDC / L-MAC-U-Adobe-AcrobatCDPro)\nIf missing AD group, request Adobe Pro via Approved Software\nClear credentials from Credential Manager (Windows/Web credentials)\nLaunch Adobe Distiller once and close\nSign out and sign back into Adobe Acrobat\nPerform Repair Installation from Help menu\nRestart system and test\nReinstall Adobe Acrobat`,
            escalation: 'ITSM-Process-SoftwareAssetMgmt (licensing issue)'
        },
        {
            error: '"License has expired or not been activated"',
            short: 'Adobe Acrobat (Reader / Pro) - error - "License has expired or not been activated"',
            steps: `End all Acrobat processes and relaunch\nVerify AD group for Adobe Pro license\nRequest/install Adobe Pro if AD group missing\nClear Credential Manager entries\nLaunch Adobe Distiller and close\nSign out/in Adobe\nRepair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'ITSM-Process-SoftwareAssetMgmt'
        },
        {
            error: '"A running instance of Acrobat has caused an error"',
            short: 'Adobe Acrobat (Reader / Pro) - error - "A running instance of Acrobat has caused an error"',
            steps: `End all Acrobat processes from Task Manager\nRelaunch and verify\nPerform Repair Installation\nRestart system\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: '"Your request is on its way"',
            short: 'Adobe Acrobat (Reader / Pro) - error - "Your request is on its way"',
            steps: `End all Acrobat processes\nVerify AD group for Adobe Pro\nIf missing, escalate to TSD Ops for software request\nSign out from adobe.com and sign back in app\nRetest issue`,
            escalation: 'ITSM-Process-SoftwareAssetMgmt'
        },
        {
            error: 'Failing to load/crashing',
            short: 'Adobe Acrobat (Reader / Pro) - launch/install - failing to load/crashing',
            steps: `End all Acrobat processes\nReset default browser (Edge)\nRestart system\nLaunch Adobe Distiller\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: 'Failing to install',
            short: 'Adobe Acrobat (Reader / Pro) - launch/install - Failing to install',
            steps: `Restart workstation\nAttempt install from Software Center\nReinstall Acrobat completely`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: 'Adobe icon missing / not installed',
            short: 'Adobe Acrobat (Reader / Pro) - launch/install - Adobe icon is missing / not installed',
            steps: `Verify required AD group\nRequest/install software if missing\nManually create shortcut via ProgramData path\nRestart workstation\nReinstall Acrobat`,
            escalation: 'ITSM-TSD-IT-REMOTE-SUPPORT'
        },
        {
            error: 'Unable to combine PDFs',
            short: 'Adobe Acrobat (Reader / Pro) - deviation - Unable to combine PDFs',
            steps: `Verify user has Acrobat Pro (not Reader)\nEnd Acrobat processes\nDisable “Save as PDF Portfolio” option\nRepair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: 'Issues opening PDFs from network drive',
            short: 'Adobe Acrobat (Reader / Pro) - deviation - Issues with opening PDFs from a network drive',
            steps: `End Acrobat processes\nClose all MS apps (Outlook, Word, Teams, etc.)\nDisable online storage & security settings in preferences\nRepair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: 'Unable to sign a document',
            short: 'Adobe Acrobat (Reader / Pro) - deviation - Unable to sign a document',
            steps: `Set Adobe as default PDF application\nRepair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: '"Print to PDF" feature missing',
            short: 'Adobe Acrobat (Reader / Pro) - deviation - "Print to PDF" feature is missing',
            steps: `Repair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: 'Redaction tool inaccurate',
            short: 'Adobe Acrobat (Reader / Pro) - deviation - Redaction tool is inaccurate',
            steps: `Verify user has Acrobat Pro\nToggle New UI (disable/enable)\nRepair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'Generic Software Escalation'
        },
        {
            error: 'Repeat Login Prompts',
            short: 'Adobe Acrobat - Repeat Login Prompts',
            steps: `Enable New Acrobat UI\nClear Credential Manager entries\nReset default browser\nRestart workstation\nFull uninstall and reinstall Acrobat`,
            escalation: 'Tier 1: ITSM-TSD-IT-REMOTE-SUPPORT\nTier 2: ITSM-TSD-IT-TEAMMATE-ENABLEMENT'
        },
        {
            error: 'Undocumented issue',
            short: 'Adobe Acrobat (Reader / Pro) - UNDC - (custom issue)',
            steps: `Verify AD group permissions\nRequest software if missing\nClear Credential Manager\nLaunch Adobe Distiller\nSign out/in Adobe\nRepair installation\nRestart system\nReinstall Acrobat`,
            escalation: 'ITSM-Process-SoftwareAssetMgmt'
        }
    ],
    "Enterprise Teller": [
        {
            error: '"Scanner Connection Error" / "Scanner Reboot Required"',
            short: 'Enterprise Teller - Check Scanners & Receipt Printers - "Scanner Connection" error',
            steps: `Verify workstation type (VDI / Windows Desktop) and capture WSID\nCollect scanner & printer serial numbers and update CI in ticket\nCheck network connectivity/configurations (section n644)\nAccess scanner admin GUI via SSE URL (browser test)\nIf loads → capture screenshot and escalate accordingly\nIf not → proceed to network troubleshooting\nRestart INET modem (30 seconds unplug/plug)\nRe-login to ET and test scanning\nRemap scanner/printer if needed`,
            escalation: 'Admin GUI loads → ITSM-RTAS-CB-EnterpriseTeller\nGUI fails → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nIf still unresolved → ITSM-RTAS-CB-EnterpriseTeller'
        },
        {
            error: '"please place item to be scanned in the scanner"',
            short: 'Enterprise Teller - Check Scanners & Receipt Printers - "please place item to be scanned" error',
            steps: `Fully sign out and close ET correctly\nPower cycle scanner\nRun cleaning mode using cleaner card\nRe-login and test scan\nRestart workstation / reset VDI (based on device type)\nPower cycle printer + scanner and reset printer config\nCheck ET config profile\nRetrieve scanner logs`,
            escalation: 'Tier 1 → ITSM-TSD-IT-REMOTE-SUPPORT\nTier 2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier 3 → ITSM-RTAS-CB-EnterpriseTeller'
        },
        {
            error: '"Scanner Not Enabled"',
            short: 'Enterprise Teller - Check Scanners & Receipt Printers - "Scanner Not Enabled"',
            steps: `Verify network connectivity/configuration\nFollow network troubleshooting (n644)\nValidate workstation type\nEnsure ET session properly closed`,
            escalation: 'If unresolved → Standard 3-tier escalation path'
        },
        {
            error: '"Last Item Jammed and Did Not Scan Properly"',
            short: 'Enterprise Teller - Check Scanners & Receipt Printers - "Last Item Jammed"',
            steps: `Sign out and close ET\nRemove jammed document\nRun cleaning card & compressed air cleaning\nRotate scanner separator (blue triangle)\nEnsure proper document alignment\nRestart workstation / VDI\nPower cycle devices and reset printer\nRetrieve scanner logs`,
            escalation: 'Tier 1 → Remote Support\nTier 2 → Teammate Enablement\nTier 3 → Enterprise Teller team'
        },
        {
            error: '"Receipt printer error"',
            short: 'Enterprise Teller - Check Scanners & Receipt Printers - "receipt printer error"',
            steps: `Verify paper availability and no jams\nFollow device-type specific steps\nSign out and close ET properly\nRemap printer (VDI)\nCheck network configuration`,
            escalation: 'Network/config unresolved → escalate via standard 3-tier path'
        },
        {
            error: '"Cashbox in use"',
            short: 'Enterprise Teller - cashbox - "Cashbox in use"',
            steps: `Educate user on proper ET logoff\nSign out properly and relaunch\nLogin without cashbox →Reset cashbox via Admin (manager) → logout → relogin with cashbox\nReset Edge browser\nOption: if not fix manger need to do office close/reopen process`,
            escalation: 'Tier 1 → Remote Support → Tier 2 → Team Enablement → Tier 3 → ET Team'
        },
        {
            error: '"Network Communication Error"',
            short: 'Enterprise Teller - login/launch - "Network Communication Error"',
            steps: `Collect scanner & printer serial numbers\nAdd CI to ticket\nFollow network troubleshooting (n644)\nValidate connectivity/config`,
            escalation: 'Standard escalation path (Tier 1 → Tier 3)'
        },
        {
            error: '"SignOn Error: An error occurred during signon"',
            short: 'Enterprise Teller - login/launch - "SignOn Error"',
            steps: `Sign out and close ET properly\nVerify AD group access (Get-ETAccess)\nReset Edge browser\nRestart workstation / reset VDI`,
            escalation: 'Tier 1 → Tier 2 → Tier 3'
        },
        {
            error: '"Workstation Error: Workstation is not initialized"',
            short: 'Enterprise Teller - login/launch - "Workstation not initialized"',
            steps: `Sign out and close ET\nCreate ET branch profile\nRestart workstation / VDI\nReset Edge browser`,
            escalation: 'Standard escalation path'
        },
        {
            error: '"FINDSTR: Cannot open"',
            short: 'Enterprise Teller - login/launch - "FINDSTR: Cannot open"',
            steps: `No troubleshooting required\nCollect branch details (property code, city, state)`,
            escalation: 'Direct assign to ITSM-RTAS-CB-EnterpriseTeller'
        },
        {
            error: '"Incomplete Customer Session Detected"',
            short: 'Enterprise Teller - balance / transaction - "Incomplete Customer Session Detected"',
            steps: `Click warning → OK\nOpen transaction list\nClose incomplete transactions (auto reverse)\nReprocess transaction`,
            escalation: 'Tier 1 → Tier 2 → Tier 3 if unresolved'
        },
        {
            error: '"ID Scan Failed"',
            short: 'Enterprise Teller - ID scanning - "ID Scan Failed"',
            steps: `Verify ID validity (not expired, correct type)\nEnsure proper placement/alignment\nRetry scan\nClean scanner\nTry alternate orientation\nRetrieve logs`,
            escalation: 'Single ID → manual entry & close\nMultiple IDs issue → ITSM-TSD-IT-TEAMMATE-ENABLEMENT'
        },
        {
            error: '"Enterprise Teller Install in Progress"',
            short: 'Enterprise Teller - login/launch - "Install in Progress"',
            steps: `Refresh Software Center policies\nCheck install status\nRestart device\nAllow up to 1 hour for install`,
            escalation: 'If failed twice/unresolved → Tier 1 → Tier 3 escalation'
        }
    ],
    "Microsoft Outlook": [
        {
            error: '"Missing emails/folders"',
            short: 'Microsoft Outlook - emails - Missing emails/folders',
            steps: `Check folder collapse/expand arrows to ensure folders are visible\nClear filters (View → View Settings → Filter → Clear All)\nCheck Online Archive for moved emails\nVerify retention policy via BEAT tool\nCheck emails in Outlook Webmail\nRestore from Deleted Items / Recover Deleted Items\nNon-persistent VDI: reset VDI → rebuild profile\nWindows/Persistent VDI: reset view → rebuild Outlook profile\nRun Outlook.exe /resetnavpane\nRun Outlook.exe /safe and restart Outlook\nRestart system and reconnect VPN\nRepair/reinstall Office`,
            escalation: 'If issue in Webmail → ITSM-Collaboration-ExchangeAndEmailSecurity (include email details)\nIf device-specific → Software Escalation'
        },
        {
            error: '"Restore deleted items"',
            short: 'Microsoft Outlook - emails - restore deleted items',
            steps: `Check Deleted Items folder\nUse Recover Deleted Items option\nRestore emails manually\nUse Webmail for bulk restore (>50 items)\nVerify retention policy restrictions`,
            escalation: 'No escalation if permanently deleted beyond retention (cannot be recovered)'
        },
        {
            error: '"An internal support function returned an error"',
            short: 'Microsoft Outlook - emails - "An internal support function returned an error"',
            steps: `Test sending email via Webmail\nCheck for invalid/duplicate email addresses\nSend emails individually to isolate issue\nNon-persistent VDI: reset + rebuild profile\nWindows: reset view → rebuild profile → resetnavpane → safe mode → restart → repair Office`,
            escalation: 'If issue in Webmail → ITSM-Collaboration-ExchangeAndEmailSecurity\nOtherwise → Software Escalation'
        },
        {
            error: '"You don\'t have permission to send to:"',
            short: 'Microsoft Outlook - emails - "You don\'t have permission to send to:"',
            steps: `Verify group mailbox attestation status\nConfirm mailbox not locked\nContact mailbox owner\nReview ownership and permissions`,
            escalation: 'No escalation; user must contact mailbox owner/team'
        },
        {
            error: 'Unable to send emails, no errors',
            short: 'Microsoft Outlook - emails - Unable to send emails, no errors',
            steps: `Check DLP or email gateway responses\nTest sending from Webmail\nNon-persistent VDI: reset + rebuild profile\nWindows: reset view → rebuild profile → resetnavpane → safe mode → restart → repair Office`,
            escalation: 'If blocked → follow DLP/Gateway escalation\nIf persists → Software Escalation or Exchange team'
        },
        {
            error: 'Failing to receive emails',
            short: 'Microsoft Outlook - emails - Failing to receive emails',
            steps: `Check Metered Connection warning\nVerify if sender gets block notification\nCheck Webmail\nCheck quarantine (Proofpoint)\nDisable Outlook rules\nNon-persistent VDI: reset + rebuild profile\nWindows: reset view → rebuild profile → resetnavpane → safe mode → restart → repair Office`,
            escalation: 'If issue in Webmail → ITSM-Collaboration-ExchangeAndEmailSecurity\nIf rules/quarantine issues unresolved → escalate with sender details'
        },
        {
            error: '"Cannot start Outlook"',
            short: 'Microsoft Outlook - Launch/Login - "Cannot start Outlook"',
            steps: `Cannot start Outlook\nUpdate Outlook\nDisable Metered Connection\nClear credentials (Credential Manager)\nReset view settings\nRebuild Outlook profile\nRun Outlook.exe /resetnavpane\nRun Outlook.exe /safe\nRestart system\nRepair/reinstall Office`,
            escalation: 'If persists → Software Escalation'
        },
        {
            error: '"Cannot open the Outlook window"',
            short: 'Microsoft Outlook - Launch/Login - "Cannot open the Outlook window"',
            steps: `Update Office\nDisable Metered Connection\nRemove credentials\nReset View\nRebuild profile\nRun resetnavpane and safe mode\nRestart system\nRepair Office`,
            escalation: 'Software Escalation'
        },
        {
            error: '"Unlicensed Product"',
            short: 'Microsoft Outlook - Launch/Login - "Unlicensed Product"',
            steps: `Check AD group (AAG-M365-LIC-OAPPS / E5)\nUpdate Office\nDisable Metered Connection\nClear credentials\nReset view\nRebuild profile\nRestart device\nRepair Office`,
            escalation: 'If license missing → ITSM-Collaboration-M365\nIf persists → Software escalation'
        },
        {
            error: '"We Can\'t Connect You (HTTP 404)"',
            short: 'Microsoft Outlook - Launch/Login - "We Can\'t Connect You (HTTP 404)"',
            steps: `Sign out and sign back into Outlook\nClose all Office apps\nReopen Outlook\nNon-persistent VDI: reset + rebuild profile\nWindows: update → clear credentials → rebuild profile → resetnavpane → safe mode → restart → repair`,
            escalation: 'Software Escalation'
        },
        {
            error: 'Mailbox Is Not Listed',
            short: 'Microsoft Outlook - Group mailboxes - Mailbox Is Not Listed',
            steps: `Verify mailbox permissions (Access For)\nConfirm mailbox exists\nRequest access if required\nNon-persistent VDI: reset + rebuild profile\nWindows: reset view → rebuild profile → resetnavpane → safe mode → restart → repair`,
            escalation: 'If mailbox deleted → no recovery\nOtherwise → Software Escalation'
        },
        {
            error: 'Add-in disabled',
            short: 'Microsoft Outlook - Add-ins - Disabled add-in',
            steps: `Open Outlook → File → Options\nNavigate to Add-ins\nSelect Disabled Items from Manage dropdown\nClick Go → Enable required add-in\nRestart Outlook`,
            escalation: 'If add-in keeps disabling → Software Escalation'
        },
        {
            error: 'Emails older than 3 months not visible',
            short: 'Microsoft Outlook - Group mailbox - Emails older than 3 months not visible',
            steps: `Check if user is part of AD group G-App-Outlook-SharedMailoxCaching\nIf yes → request removal from AD group\nWait 4 hours for update\nDelete registry key SharedMailboxCacheEnabled\nRestart system\nRebuild Outlook profile`,
            escalation: 'Tier 1 → Warm transfer to Remote Support\nIf needed → Exchange/Support team'
        },
        {
            error: 'Unread emails count increases but emails not visible',
            short: 'Microsoft Outlook - Group mailbox - Unread emails not visible',
            steps: `Access mailbox via Outlook Web App\nOpen mailbox using "Open another mailbox"\nIdentify emails marked Private/Confidential`,
            escalation: 'No escalation (Known issue, no fix)'
        },
        {
            error: 'Quarantined emails missing after 10 days',
            short: 'Microsoft Outlook - emails - Quarantined emails missing',
            steps: `Check Proofpoint portal\nVerify deletion timeline (10 days retention)`,
            escalation: 'Not possible (permanent deletion)'
        },
        {
            error: '"Group only accepts messages from allowed list"',
            short: 'Microsoft Outlook - emails - DL restricted sending',
            steps: `Identify DL owner\nRequest owner to submit access request\nSubmit “All Other Email Requests” form`,
            escalation: 'DL Owner / Email Services Team'
        },
        {
            error: 'Emails sent from group mailbox show individual sender',
            short: 'Microsoft Outlook - emails - Group mailbox sent as user',
            steps: `Close Outlook, Teams, Jabber\nRun registry command: DelegateSentItemsStyle=1\nRestart Outlook\nRestart system if needed\nNon-persistent/Windows: rebuild profile`,
            escalation: 'If persists → Software Escalation'
        },
        {
            error: 'Emails blocked by DLP/Gateway',
            short: 'Microsoft Outlook - emails - Sent emails blocked',
            steps: `Identify blocking email source\nIf DLP → contact Infosec-DLP\nIf Gateway → collect details (recipient, time, subject, screenshot)`,
            escalation: 'Assign to ITSM-Collaboration-ExchangeAndEmailSecurity'
        },
        {
            error: '"IMCEAEX-_o=ExchangeL" error',
            short: 'Microsoft Outlook - emails - IMCEAEX error',
            steps: `Compose new email\nType recipient name\nRemove cached entry\nRe-enter email manually\nResend email`,
            escalation: 'Software Escalation if persists'
        },
        {
            error: '"Maximum number of recipients exceeded"',
            short: 'Microsoft Outlook - emails - Too many recipients',
            steps: `Verify recipient count (<500)\nUse Distribution List instead\nSplit email into multiple sends`,
            escalation: 'Not applicable (policy restriction)'
        },
        {
            error: 'Emails auto marked secure',
            short: 'Microsoft Outlook - emails - Auto secure emails',
            steps: `Verify user role/policy restriction\nInform user behavior controlled by role\nSuggest workaround`,
            escalation: 'No escalation (policy controlled)'
        },
        {
            error: 'DL not receiving external emails',
            short: 'Microsoft Outlook - emails - DL not receiving external emails',
            steps: `Check DL attribute CustomAttribute14\nIf blank → request enable external emails\nValidate via BEAT tool`,
            escalation: 'DL Owner / Email Services'
        },
        {
            error: 'No access to group mailbox',
            short: 'Microsoft Outlook - Group mailbox - Access issue',
            steps: `Verify permissions in BEAT tool\nCheck Access For section\nRequest mailbox access`,
            escalation: 'Mailbox owner / access request'
        },
        {
            error: 'Private/Confidential emails not visible',
            short: 'Microsoft Outlook - emails - Sensitivity restriction',
            steps: `Open mailbox in Webmail\nVerify sensitivity classification\nInform sender to avoid Private/Confidential\nCheck Outlook send settings`,
            escalation: 'Not applicable (Microsoft limitation)'
        },
        {
            error: 'Email notifications not received',
            short: 'Microsoft Outlook - emails - Notifications not working',
            steps: `Non-persistent VDI: reset + rebuild profile\nWindows: reset view → rebuild profile → resetnavpane → safe mode\nRestart system\nRepair Office`,
            escalation: 'If persists → Software Escalation'
        },
        {
            error: '"Couldn\'t Verify Account"',
            short: 'Microsoft Outlook - Login - Couldn\'t verify account',
            steps: `Check AD license group (E5)\nUpdate Outlook\nClear credentials\nReset view\nRebuild profile\nRestart system\nRepair Office`,
            escalation: 'If no license → ITSM-Collaboration-M365\nElse → Software Escalation'
        },
        {
            error: 'OST file corrupted',
            short: 'Microsoft Outlook - Launch/Login - OST file error',
            steps: `Update Outlook\nClear credentials\nReset view\nRebuild Outlook profile (creates new OST file)\nRestart system\nRepair Office`,
            escalation: 'Software Escalation'
        },
        {
            error: '"Start Outlook in safe mode"',
            short: 'Microsoft Outlook - Launch/Login - Safe mode prompt',
            steps: `Update Office\nDisable Metered connection\nClear credentials\nReset view\nRebuild profile\nRun Outlook safe mode test\nRestart system\nRepair Office`,
            escalation: 'Software Escalation'
        },
        {
            error: '"Not enough memory"',
            short: 'Microsoft Outlook - Launch/Login - Memory error',
            steps: `Close background apps\nUpdate Outlook\nClear credentials\nReset view\nRebuild profile\nRestart system\nRepair Office`,
            escalation: 'Software Escalation'
        }
    ],
    "Microsoft Teams": [
        {
            error: '"Your account is blocked"',
            short: 'Microsoft Teams - Error: "Your account is blocked"',
            steps: `Reset Teams app (Windows/persistent VDI → KB reset steps / non‑persistent VDI → full VDI reset)\nRestart workstation and re-login\nVerify issue after login`,
            escalation: 'Escalate to ITSM-InfoSec-Azure-IAM-Operations'
        },
        {
            error: '"We Can\'t Connect You"',
            short: 'Microsoft Teams - launch / login issues - "We Can\'t Connect You" error',
            steps: `Reset Teams app (device-based: Windows/VDI)\nRepeat reset for persistent devices\nRestart workstation\nTest on Teams web (https://teams.microsoft.com.mcas.ms/v2/)`,
            escalation: 'Web issue → ITSM-Collaboration-Teams\nLocal issue → Software Escalation (dp5d)'
        },
        {
            error: '"Something went wrong (135011 / 700003)"',
            short: 'Microsoft Teams - launch / login issues - Something went wrong error',
            steps: `Clear extra credentials in Credential Manager\nRun dsregcmd /leave and restart\nReset Teams app\nRestart system\nCheck Teams web version`,
            escalation: 'Web issue → ITSM-Collaboration-Teams\nLocal issue → Software Escalation'
        },
        {
            error: '"You Cannot Access This Right Now" (Mobile/Mac)',
            short: 'Microsoft Teams - launch/login issues - “You Cannot Access This Right Now”',
            steps: `Check geo restrictions (restricted country)\nVerify Intune installed\nValidate correct app source (Work Play Store / Intune app)\nConfirm device type (Android/iOS/Mac)`,
            escalation: 'Escalate to ITSM-Collaboration-Teams'
        },
        {
            error: '"You don\'t have required access permission"',
            short: 'Microsoft Teams - access permission issue',
            steps: `Check AD group (E5 required, E3 no access)\nVerify LOA timing (<24 hrs wait)\nReset Teams app\nRestart device\nTest web version`,
            escalation: 'Web issue → ITSM-Collaboration-Teams\nLocal issue → Software Escalation'
        },
        {
            error: 'Failing to launch / no error',
            short: 'Microsoft Teams - launch / login issues - failing to launch',
            steps: `Reset Teams app\nRepeat reset on persistent systems\nRestart workstation`,
            escalation: 'Software Escalation'
        },
        {
            error: 'Microphone not working',
            short: 'Microsoft Teams - audio issue - mic not working',
            steps: `Verify mic in Windows Sound settings\nValidate Teams device settings\nCheck microphone privacy permissions\nPerform Teams test call\nReinstall drivers (Windows 11)\nReset Teams app\nRestart system and reconnect device`,
            escalation: 'Calls issue → ITSM-Ops-EnterpriseVoice\nMeetings/audio → ITSM-AudioVisualSupport'
        },
        {
            error: 'No sound can be heard',
            short: 'Microsoft Teams - audio issue - no sound',
            steps: `Check system sound (volume test)\nVerify Teams speaker settings\nCheck Sound Mixer levels\nPerform Teams test call\nUpdate drivers if needed\nReset Teams and restart`,
            escalation: 'Calls issue → ITSM-Ops-EnterpriseVoice\nMeetings/audio → ITSM-AudioVisualSupport'
        },
        {
            error: 'Unable to delete chats',
            short: 'Microsoft Teams - chat issue - unable to delete conversations',
            steps: `Check AD group (SEC-6year-BBT-Securities)\nVerify Wealth LOB restriction\nReset Teams app\nTest web version`,
            escalation: 'ITSM-Collaboration-Teams (if web issue)'
        },
        {
            error: 'Unable to use GIFs',
            short: 'Microsoft Teams - chat issue - unable to use GIFs',
            steps: `Confirm not on VDI (GIFs unsupported)\nCheck AD restriction group\nVerify “Optional connected experiences” ON\nReset Teams app\nTest web version`,
            escalation: 'ITSM-Collaboration-Teams'
        },
        {
            error: '"Sorry your company policy prevents you from joining this call"',
            short: 'Microsoft Teams - meetings - policy restriction',
            steps: `Confirm no channel access\nAsk user to contact meeting owner\nRequest addition to channel OR meeting reschedule`,
            escalation: '❌ No escalation (close after guidance)'
        },
        {
            error: '"There\'s a Problem With Your Connection"',
            short: 'Microsoft Teams - meetings - connection issue',
            steps: `Reset Teams app\nRestart workstation\nCheck VDI environment (test VDI limitations)\nTest web version`,
            escalation: 'Web issue → ITSM-Collaboration-Teams\nLocal issue → Software Escalation'
        },
        {
            error: 'Unable to join meeting (no error)',
            short: 'Microsoft Teams - meetings - unable to join',
            steps: `Reset Teams app\nRestart device\nCheck VDI type\nTest web version`,
            escalation: 'Web issue → ITSM-Collaboration-Teams'
        },
        {
            error: 'Unable to screenshare',
            short: 'Microsoft Teams - meetings - unable to screenshare',
            steps: `Check AD restriction group (Accenture/Wealth)\nReset Teams app\nRestart workstation\nUpdate graphics drivers\nCheck VDI environment\nTest web version`,
            escalation: 'ITSM-Collaboration-Teams'
        },
        {
            error: 'Double Status (Available + OOO)',
            short: 'Microsoft Teams - status issue - multiple status',
            steps: `Check Outlook meeting “Show As” status\nUpdate incorrect meetings\nDecline OOO meetings if needed\nRestart Outlook + Teams\nReset Teams app`,
            escalation: 'ITSM-Collaboration-Teams'
        },
        {
            error: 'Unable to place calls',
            short: 'Microsoft Teams - calling issue - unable to dial numbers',
            steps: `Check AD groups (PhoneSystem + Voice-EndUser)\nRestart workstation (policy sync)\nReset Teams app\nValidate VDI type`,
            escalation: 'ITSM-Ops-EnterpriseVoice'
        },
        {
            error: 'Teams not installed',
            short: 'Microsoft Teams - application missing',
            steps: `Search app in system\nUse web version (temporary)\nDownload from Microsoft site`,
            escalation: 'Local application escalation if install fails'
        },
        {
            error: 'Undocumented issue (Teams)',
            short: 'Microsoft Teams - UNDC - (issue description)',
            steps: `Reset Teams app\nRestart device\nCheck web version\nValidate device type & AD groups`,
            escalation: 'Web issue → ITSM-Collaboration-Teams\nLocal issue → Software Escalation'
        }
    ],
    "Virtual Desktop (VDI)": [
        {
            error: '"copy / paste is not working"',
            short: 'Virtual Desktop (VDI) - misc. - copy / paste is not working',
            steps: `Identify VDI type (PD/ND/PDU/NDU) and environment\nLogin to Citrix Director (prod/dev based on VDI)\nCheck Policies tab → verify EXTERNAL ACCESS policies\nIf external access → expected behavior (vendor device restriction)\nIf internal → reset/reinstall Citrix Workspace\nRetest copy/paste`,
            escalation: 'Tier1 → ITSM-TSD-IT-REMOTE-SUPPORT\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT'
        },
        {
            error: '"Low Disk Space"',
            short: 'Virtual Desktop (VDI) - misc. - Low Disk Space',
            steps: `Open Storage Settings → enable Storage Sense\nRemove unused apps / raise request for removal\nDelete Temporary files from settings\nClear %temp% folder (select all → delete → skip locked files)\nRun OneDrive “Free up space”\nRun cleanmgr /sageset and /sagerun\nDelete CrashDumps folder\nRebuild Indexing\nMove large files (>5GB) to OneDrive root`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        },
        {
            error: '"Login Failed, Try Again or Contact Help Desk"',
            short: 'Virtual Desktop (VDI) - login - "Login Failed, Try Again or Contact Help Desk"',
            steps: `Check RSA authentication logs\nValidate successful token entries\nCheck account status (locked/expired/sabbatical) in PowerShell\nReset/unlock password if required\nValidate correct login method (updated URLs)`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT'
        },
        {
            error: '"Gateway Timeout"',
            short: 'Virtual Desktop (VDI) - login - "Gateway Timeout"',
            steps: `Confirm user is on vendor workstation\nEnsure vendor VPN is connected\nRetry accessing partner URL\nIf still failing → vendor must whitelist site / update firewall`,
            escalation: 'Vendor support (primary)\nNo internal fix beyond guidance'
        },
        {
            error: '"Unapproved Access"',
            short: 'Virtual Desktop (VDI) - login - "Unapproved Access"',
            steps: `Verify correct URL (partners vs deprecated links)\nConfirm vendor workstation + VPN\nValidate firewall/whitelisting\nCheck third-party communication link setup`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        },
        {
            error: '"Cannot start desktop"',
            short: 'Virtual Desktop (VDI) - launch - "Cannot start desktop"',
            steps: `Identify VDI type & name\nLogin to Director (prod/dev/DR)\nCheck system message\nFollow respective error path\nRestart VDI\nRetest login`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        },
        {
            error: 'There are no apps or desktops available',
            short: 'Virtual Desktop (VDI) - launch - no VDIs available',
            steps: `Check if Dev VDI accessed via browser (not Workspace)\nVerify VDI request in ServiceNow\nCheck request status (Approval / Completed)\nValidate correct environment access\nConfirm provisioning`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        },
        {
            error: '"Temporarily unavailable due to planned maintenance"',
            short: 'Virtual Desktop (VDI) - launch - maintenance mode',
            steps: `Check active INC tickets\nVerify if maintenance intentional\nDisable maintenance mode in Director\nRestart VDI\nRetest`,
            escalation: 'Assign to ITSM-VDI SUPPORT'
        },
        {
            error: '"Exceeded concurrent connection limit"',
            short: 'Virtual Desktop (VDI) - launch - concurrent session limit',
            steps: `Identify VDI and user\nEnd all active sessions in Director\nRestart VDI\nClear browser cache\nRetry login`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        },
        {
            error: 'Performance Issue (Slowness/Freezing)',
            short: 'Virtual Desktop (VDI) - performance - freezing/slowness',
            steps: `Identify VDI & environment\nCheck latency and ping \nClear AppData temp folder\nRestart VDI from director \ncheck latency on director if latency more that 250 ms Tm need to contact local it help desk \n(local it help desk need to check vpn network speed network performance and citrix reinstall and outside vdi browser reset )`,
            escalation: 'Tier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT'
        },
        {
            error: 'Audio Issue (No Sound)',
            short: 'Virtual Desktop (VDI) - audio - no sound',
            steps: `Check mute and volume\nVerify correct audio device\nCheck Citrix Preferences (audio redirection)\nTest sound in app and browser by male test call \nfor test call open app > open setting > device > test call\nRestart VDI\ncheck on director teams optimize status \nif no optimize reinstall citrix`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        },
        {
            error: 'Custom / Unknown (VDI)',
            short: 'Virtual Desktop (VDI) - UNDC - ("exact issue")',
            steps: `Capture exact error\nCheck RSA / account status\nVerify VPN / access method\nReset Citrix Workspace\nReset browser\nRestart VDI`,
            escalation: 'Tier1 → Warm transfer\nTier2 → ITSM-TSD-IT-TEAMMATE-ENABLEMENT\nTier3 → ITSM-VDI SUPPORT'
        }
    ]
};

function populateIssues() {
    const appSelect = document.getElementById('targetApp');
    const issueSelect = document.getElementById('issueError');
    const selectedApp = appSelect.value;

    issueSelect.innerHTML = '<option value="">-- Select Error/Issue --</option>';
    document.getElementById('shortDesc').value = '';
    document.getElementById('tsSteps').value = '';
    document.getElementById('escalationText').innerText = 'Select an application and issue to see escalation path.';

    if (selectedApp && knowledgeBase[selectedApp]) {
        knowledgeBase[selectedApp].forEach((item, index) => {
            let opt = document.createElement('option');
            opt.value = index;
            opt.text = item.error;
            issueSelect.appendChild(opt);
        });
    }
}

function populateIssueDetails() {
    const appSelect = document.getElementById('targetApp').value;
    const issueIndex = document.getElementById('issueError').value;

    if (appSelect && issueIndex !== "") {
        const selectedIssue = knowledgeBase[appSelect][issueIndex];
        document.getElementById('shortDesc').value = selectedIssue.short;
        document.getElementById('tsSteps').value = selectedIssue.steps;
        document.getElementById('escalationText').innerText = selectedIssue.escalation;
    }
}

function generateTemplate() {
    const userId = document.getElementById('userId').value || "N/A";
    const userName = document.getElementById('userName').value || "N/A";
    const callbackNum = document.getElementById('callbackNum').value || "N/A";
    const workLocation = document.getElementById('workLocation').value || "N/A";
    const shiftTime = document.getElementById('shiftTime').value || "N/A";
    const deviceType = document.getElementById('deviceType').value || "N/A";
    const wsid = document.getElementById('wsid').value || "N/A";
    const targetApp = document.getElementById('targetApp').value || "N/A";
    const issueError = document.getElementById('issueError').options[document.getElementById('issueError').selectedIndex]?.text || "N/A";
    const shortDesc = document.getElementById('shortDesc').value || "N/A";
    const tsSteps = document.getElementById('tsSteps').value || "N/A";

    const template = `==================================================
IT SERVICE DESK TICKET TEMPLATE
==================================================
[TEAMMATE INFORMATION]
User ID            : ${userId}
User Name          : ${userName}
Call Back Number   : ${callbackNum}
Work Location      : ${workLocation}
Shift Time         : ${shiftTime}

[DEVICE & ENVIRONMENT DETAILS]
Device Type        : ${deviceType}
Workstation ID     : ${wsid}

[APPLICATION ERROR METADATA]
Target Application : ${targetApp}
Issue / Error      : ${issueError}
Short Description  : ${shortDesc}

[TROUBLESHOOTING STEPS PERFORMED]
${tsSteps}
==================================================
Generated via Template Generator by Sandip Payghan
==================================================`;

    document.getElementById('outputTemplate').value = template;
}

function saveToCDrive() {
    generateTemplate();
    const textData = document.getElementById('outputTemplate').value;
    if (!textData.trim()) {
        alert("Please generate the template first before downloading.");
        return;
    }
    
    const blob = new Blob([textData], { type: 'text/plain' });
    const link = document.createElement('a');
    link.download = 'sandip.txt';
    link.href = window.URL.createObjectURL(blob);
    link.style.display = 'none';
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
}
</script>

</body>
</html>
