Prepare for DeploymentYou’re using a content-copy folder for deployment to avoid committing the symlink (content). Ensure it’s up-to-date and that quartz.config.ts is configured correctly.Actions:

### Update content-copy:
- Refresh the copy:
        
	```
	rmdir /s /q C:\Users\user\quartz\content-copy
	mkdir C:\Users\user\quartz\content-copy
	xcopy "C:\Users\user\iCloudDrive\iCloud~md~obsidian\RealityHub\*"
	C:\Users\user\quartz\content-copy\ /E /H /C /I
	```  
- Remove sensitive files (e.g., .obsidian/).

### Build the Site:

- Run:
    
    ```text
    npx quartz build
    ```
    
- Check for errors in the output.

### Commit and Push:

- Stage and commit:
    
    ```text
    git add .
    git commit -m "Initial Quartz setup with vault copy"
    git push -u origin main
    ```