# FAQ

## Data is private

Any datastore you upload to Grid can only be accessed **by you**. Grid does not look at or manipulate your data in anyway. 

## Data retention

If you delete your account, data will be deleted immediately.

## Public vs private data

When you create a datastore, you certify that you have the rights to that data. Only you have access to your datastore. It's up to you to make sure you have the rights to access that data.

## Does Grid charge for Data Storage?

Grid does not charge for storing data. However, there is a limit of 25 datastores.

## Is there a way to see what files are in a datastore?

Create an interactive session with the datastore mounted, then you will be able to browse the data including folders and files using Jupyter lab or SSH

## How does Grid store/access my data?

Grid will have access to your account data for operational purposes. If we do need access to your account for debugging purposes, we will notify you.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Data type</th>
      <th style="text-align:left">Grid Access</th>
      <th style="text-align:left">Storage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Datasets</td>
      <td style="text-align:left">
        <p>Only your account can access your data.</p>
        <p>Grid and its service providers only access your data for operational purposes,
          including providing the services and support to you.</p>
      </td>
      <td style="text-align:left">S3</td>
    </tr>
    <tr>
      <td style="text-align:left">Artifacts</td>
      <td style="text-align:left">Grid only reads metadata.</td>
      <td style="text-align:left">S3</td>
    </tr>
    <tr>
      <td style="text-align:left">Metadata</td>
      <td style="text-align:left">Information about your jobs (no code, no data).</td>
      <td style="text-align:left">Database</td>
    </tr>
  </tbody>
</table>

