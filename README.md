# web3storage-hooks

A set of React hooks for easy integration with Web3.Storage, enabling seamless interaction with the decentralized storage directly from your React applications.

## Features

- **useWeb3StorageUpload**: A React hook to simplify uploading files to Web3.Storage.
- Global Web3.Storage client management through React Context.
- Typescript support for type safety and better developer experience.

## Installation

To install the package, run the following command in your project directory:

```bash
npm install web3storage-hooks
```

If you use yarn

```
yarn add web3storage-hooks
```

### Usage

#### Setting up the Web3.Storage Provider
Wrap your application or component tree with Web3StorageProvider to make the Web3.Storage client available throughout your application.

```
import React from 'react';
import ReactDOM from 'react-dom';
import { Web3StorageProvider } from 'web3storage-hooks';
import App from './App';

  const web3StorageConfig = {
    spaceName: 'JohnSpace',
    email: 'john@doe.com',
  };

ReactDOM.render(
  <React.StrictMode>
    <Web3StorageProvider config={web3StorageConfig}>
      <App />
    </Web3StorageProvider>
  </React.StrictMode>,
  document.getElementById('root')
);
```


#### Using the useWeb3StorageUpload Hook
Here's how you can use the useWeb3StorageUpload hook to upload files to Web3.Storage.


```
import React, { useState } from 'react';
import { useWeb3StorageUpload } from 'web3storage-hooks';

function FileUploader() {
  const [file, setFile] = useState(null);
  const { uploadFile, isUploading, uploadError, uploadResult } = useWeb3StorageUpload();

  const handleFileChange = (event) => {
    setFile(event.target.files[0]);
  };

  const handleUpload = async () => {
    if (file) await uploadFile(file);
  };

  return (
    <div>
      <input type="file" onChange={handleFileChange} />
      <button onClick={handleUpload} disabled={isUploading}>Upload to Web3.Storage</button>
      {uploadError && <p>Error: {uploadError}</p>}
      {uploadResult && <p>File uploaded successfully: {uploadResult.url}</p>}
    </div>
  );
}
```


#### Configuration Options
The Web3StorageProvider accepts a configuration object with the following options:


**email**: Your Web3.Storage account email. (required for space setup)

https://web3.storage/docs/how-to/create-space/

**spaceName**: The name of the space to be used for uploads. 

https://web3.storage/docs/how-to/create-account/

#### Contributing
Contributions are welcome! Please feel free to submit a pull request or open an issue if you have feedback, suggestions, or want to contribute to the codebase.

#### Reporting Issues
If you encounter any issues or have suggestions, please use the GitHub issues page to report them.

#### License
This project is licensed under the MIT License - see the LICENSE file for details.

