# Publishing and Upload Guide

This guide is separate from the technical implementation documents.

## A. GitHub repository

### Create the repository
1. Sign in to GitHub as `riaxkhan007`.
2. Open the New repository page: https://github.com/new
3. Repository name: `active-directory-group-policy-lab`.
4. Description: `Windows Server 2022 Active Directory, Group Policy, SMB file sharing, and workstation security lab.`
5. Set visibility to **Public** only after checking screenshots for credentials, personal information, and sensitive network details.
6. Select **Add a README file** if creating the repo from an empty browser upload workflow. If you instead upload this package's existing `README.md`, leave the initialization options off to avoid a README conflict.
7. Click **Create repository**.

### Upload through the browser
1. Open the new repository.
2. Choose **Add file > Upload files**.
3. Drag the contents of the `active-directory-group-policy-lab` folder into the upload area, or select files. Keep the folder structure (`assets`, `docs`, `publishing`, `screenshots`).
4. Review the file list and make sure `README.md` is at the repository root.
5. Add commit message: `Add Active Directory and Group Policy lab documentation`.
6. Commit the upload to the `main` branch.
7. Return to the repository home page and confirm the README renders, images load, and the docs folder is visible.

Official GitHub references:
- Create a repository: https://docs.github.com/en/get-started/start-your-journey/creating-a-repository-for-your-project-on-github
- Upload files: https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository

### Recommended repository settings
- Add the topic tags `active-directory`, `windows-server`, `group-policy`, `dns`, `file-services`.
- Keep the repository public only if the evidence is sanitized. Do not upload the original source PDF; the public package contains redacted/cropped evidence images instead.
- Do not upload passwords, DSRM recovery information, private keys, VPN configuration, personal documents, or real company screenshots.

## B. Upwork portfolio item

1. Sign in to Upwork and open **Find Work > Profile** (menu labels can vary slightly by layout).
2. Scroll to the **Portfolio** section and choose the **+ / Add a portfolio item** control.
3. Enter the title from `publishing/Upwork-Portfolio-Copy.md`.
4. Set the role to `Windows Server / Active Directory Administrator`.
5. Paste the short project description into the overview field; paste the longer description into the detailed description/media caption field if available.
6. Add up to five relevant skills from the suggested list.
7. Do not link a client contract; this was a personal lab project.
8. Upload `assets/portfolio-cover.png` first, then add a few strongest screenshots and the report PDF if the form allows it.
9. Preview the item on desktop and mobile, verify all images are readable, and publish.
10. Check the live portfolio item from your public profile.

Upwork notes: use a clear original sample, avoid contact information in the portfolio, and follow the accepted media types and size limits shown in the upload form. Current Upwork Help lists a title up to 70 characters, role up to 100 characters, and description up to 600 characters; its help center also documents image dimensions and file types. See https://support.upwork.com/hc/en-us/articles/360016144974-How-to-enhance-your-freelancer-profile and https://support.upwork.com/hc/en-us/articles/39295662788115-Why-won-t-my-portfolio-item-publish.

## C. LinkedIn post and Featured section

### Publish the document post
1. Sign in to LinkedIn and open the Home feed.
2. Click **Start a post**.
3. Choose **More** or the document attachment option, then select **Add a document**.
4. Upload `docs/Project-Overview.pdf` (or the Technical Implementation Report PDF if you prefer the full report).
5. Give the document a clear title: `Active Directory & Group Policy Lab - Technical Overview`.
6. Paste the text from `publishing/LinkedIn-Post.md` into the post description.
7. Review the preview, then select **Post**.

LinkedIn's current help says document posts support PDF, DOC/DOCX, and PPT/PPTX; uploaded documents can be up to 100 MB and 300 pages. See https://www.linkedin.com/help/linkedin/answer/a518909.

### Add the project to your profile
1. Open your LinkedIn profile.
2. Select **Add profile section > Recommended > Projects**.
3. Use the title and description from `publishing/LinkedIn-Project-Entry.md`.
4. Leave the project unassociated with an employer because it is a self-directed lab.
5. Add the overview PDF and architecture image as media if the editor offers that option.
6. Add the public GitHub repository using **Add media > Add a link** if available. LinkedIn notes that the Project URL field may not be available for newly added projects.

### Add the post and repository to Featured
1. Open your LinkedIn profile.
2. If Featured is not present, select **Add profile section > Recommended > Featured**.
3. In Featured, click **+**.
4. Choose the published LinkedIn post for the PDF overview, or add an external link to the public GitHub repository.
5. Use the title and description from `publishing/LinkedIn-Featured-Copy.md`.
6. Reorder Featured items so the technical overview and repository appear first.

LinkedIn Featured can display posts, documents, and external links. See https://www.linkedin.com/help/linkedin/answer/a553419 and https://www.linkedin.com/help/linkedin/answer/a550399/manage-featured-samples-of-your-work-on-your-linkedin-profile. For Project sections, see https://www.linkedin.com/help/linkedin/answer/a540837/add-sections-to-your-profile.

## Final publishing checklist

- [ ] Correct the elevated-installer policy before describing the security configuration as hardened.
- [ ] Review/replace the Everyone Full Control share permission.
- [ ] Update the password minimum length.
- [ ] Remove any credentials, private IPs, personal data, or company data from screenshots.
- [ ] Ensure README links and screenshots render in GitHub.
- [ ] Ensure Upwork copy does not imply paid client work or claim unverified test results.
- [ ] Ensure LinkedIn post links to the final public GitHub repository.
