# document-control-demo2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Proposal & Document Management Demo</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <style>
        :root {
            --primary: #2563eb;
            --success: #16a34a;
            --warning: #f59e0b;
            --danger: #dc2626;
            --light: #f3f4f6;
            --dark: #111827;
        }

        * {
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            margin: 0;
            background: #f9fafb;
        }

        h2, h3, h4 {
            margin: 0;
        }

        /* Layout */
        .app {
            display: flex;
            min-height: 100vh;
        }

        .sidebar {
            width: 240px;
            background: var(--dark);
            color: #fff;
            padding: 1rem;
        }

        .sidebar h3 {
            margin-bottom: 1rem;
        }

        .sidebar-menu a {
            display: block;
            padding: 0.6rem;
            color: #d1d5db;
            text-decoration: none;
            border-radius: 6px;
            margin-bottom: 0.3rem;
            cursor: pointer;
        }

        .sidebar-menu a.active,
        .sidebar-menu a:hover {
            background: #1f2937;
            color: #fff;
        }

        .content {
            flex: 1;
            padding: 1.5rem;
        }

        .page {
            display: none;
        }

        .page.active {
            display: block;
        }

        /* Cards */
        .card {
            background: #fff;
            border-radius: 10px;
            margin-top: 1rem;
            box-shadow: 0 1px 4px rgba(0,0,0,0.08);
        }

        .card-header {
            padding: 1rem;
            border-bottom: 1px solid #e5e7eb;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .card-body {
            padding: 1rem;
        }

        /* Buttons */
        .btn-sm {
            padding: 0.35rem 0.7rem;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.85rem;
        }

        .btn-view {
            background: var(--primary);
            color: #fff;
        }

        .btn-approve {
            background: var(--success);
            color: #fff;
        }

        .btn-upload {
            background: var(--primary);
            color: #fff;
            padding: 0.6rem;
            border-radius: 8px;
            border: none;
            cursor: pointer;
        }

        /* Table */
        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 0.6rem;
            border-bottom: 1px solid #e5e7eb;
            text-align: left;
        }

        th {
            background: var(--light);
        }

        /* Status */
        .status-badge {
            padding: 0.2rem 0.5rem;
            border-radius: 12px;
            font-size: 0.75rem;
            color: #fff;
        }

        .status-approved { background: var(--success); }
        .status-review { background: var(--warning); }
        .status-draft { background: #6b7280; }
        .status-final { background: var(--primary); }

        /* Document List */
        .doc-list {
            list-style: none;
            padding: 0;
        }

        .doc-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #fff;
            padding: 0.75rem;
            border-radius: 8px;
            margin-bottom: 0.6rem;
            box-shadow: 0 1px 3px rgba(0,0,0,0.08);
        }

        .doc-info {
            display: flex;
            gap: 0.75rem;
            align-items: center;
        }

        .doc-icon {
            font-size: 1.5rem;
        }

        /* Modal */
        .modal {
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.45);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 999;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: #fff;
            width: 90%;
            max-width: 600px;
            border-radius: 10px;
            overflow: hidden;
        }

        .modal-header {
            padding: 1rem;
            background: var(--light);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .modal-body {
            padding: 1rem;
        }

        .btn-close {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
        }

        .form-group {
            margin-bottom: 0.75rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.3rem;
            font-size: 0.85rem;
        }

        input, select, textarea {
            width: 100%;
            padding: 0.45rem;
            border-radius: 6px;
            border: 1px solid #d1d5db;
        }

        textarea {
            resize: vertical;
        }

        .file-upload-area {
            border: 2px dashed #c7d2fe;
            padding: 1rem;
            text-align: center;
            border-radius: 8px;
            cursor: pointer;
            background: #eef2ff;
        }
    </style>
</head>

<body>

<div class="app">
    <div class="sidebar">
        <h3>Demo Portal</h3>
        <div class="sidebar-menu">
            <a class="active" onclick="showPage('documents', event)">Documents</a>
            <a onclick="showPage('proposals', event)">Proposals</a>
        </div>
    </div>

    <div class="content">
        <!-- Documents -->
        <div id="documents" class="page active">
            <h2>Documents</h2>
            <ul class="doc-list">
                <li class="doc-item">
                    <div class="doc-info">
                        <div class="doc-icon">📄</div>
                        <div>
                            <h4>CRF (Customer Requirement Form)</h4>
                            <p>SO_2026_001_CRF_V1.pdf |
                                <span class="status-badge status-approved">APPROVED</span>
                            </p>
                        </div>
                    </div>
                    <button class="btn-sm btn-view">View</button>
                </li>
            </ul>
        </div>

        <!-- Proposals -->
        <div id="proposals" class="page">
            <h2>Design Proposals</h2>

            <div class="card">
                <div class="card-header">
                    <h3>Active Proposals</h3>
                    <button class="btn-sm btn-approve" onclick="openModal('createProposal')">+ Create</button>
                </div>

                <div class="card-body">
                    <table>
                        <thead>
                        <tr>
                            <th>SO</th>
                            <th>Customer</th>
                            <th>Version</th>
                            <th>Status</th>
                            <th>Actions</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr>
                            <td>SO/2026/001</td>
                            <td>ABC Manufacturing</td>
                            <td>V2</td>
                            <td><span class="status-badge status-review">Under Review</span></td>
                            <td>
                                <button class="btn-sm btn-view" onclick="openModal('viewProposalModal')">View</button>
                            </td>
                        </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- Create Proposal Modal -->
<div id="createProposal" class="modal">
    <div class="modal-content">
        <div class="modal-header">
            <h3>Create Proposal</h3>
            <button class="btn-close" onclick="closeModal('createProposal')">&times;</button>
        </div>
        <div class="modal-body">
            <div class="form-group">
                <label>Proposal Title</label>
                <input placeholder="Proposal title">
            </div>
            <div class="form-group">
                <label>Upload PDF</label>
                <div class="file-upload-area">Click to upload</div>
            </div>
            <button class="btn-upload" onclick="closeModal('createProposal')">Save</button>
        </div>
    </div>
</div>

<!-- View Proposal Modal -->
<div id="viewProposalModal" class="modal">
    <div class="modal-content">
        <div class="modal-header">
            <h3>Proposal Details</h3>
            <button class="btn-close" onclick="closeModal('viewProposalModal')">&times;</button>
        </div>
        <div class="modal-body">
            <p><strong>Customer:</strong> ABC Manufacturing</p>
            <p><strong>Status:</strong> Under Review</p>
            <button class="btn-upload">Release to Sales</button>
        </div>
    </div>
</div>

<script>
    function showPage(pageId, e) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById(pageId).classList.add('active');

        document.querySelectorAll('.sidebar-menu a').forEach(a => a.classList.remove('active'));
        e.target.classList.add('active');
    }

    function openModal(id) {
        document.getElementById(id).classList.add('active');
    }

    function closeModal(id) {
        document.getElementById(id).classList.remove('active');
    }
</script>

</body>
</html>
