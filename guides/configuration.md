# Configuration

## Email notifications

Giskard can send email notifications about different events like inspector feedbacks or user invitation to the platform.

To configure this feature SMTP server credentials should be provided at startup through environment variables

| Environment variable name | Purpose                                 |
| ------------------------- | --------------------------------------- |
| GISKARD\_MAIL\_HOST       | SMTP server address                     |
| GISKARD\_MAIL\_PORT       | SMTP port, 587 by default               |
| GISKARD\_MAIL\_USERNAME   |                                         |
| GISKARD\_MAIL\_PASSWORD   |                                         |
| GISKARD\_MAIL\_BASEURL    | Publicly available Giskard instance URL |
