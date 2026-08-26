Users should be able to login with Google accounts.

#### IMPLEMENTATION COMPLETE
- Backend: GoogleIdTokenIdentityVerifier verifies Google ID tokens server-side
- Frontend: AuthView displays Google sign-in button when GOOGLE_CLIENT_ID is configured
- Deployment docs document how to set GOOGLE_CLIENT_ID in environment
- .env.example shows GOOGLE_CLIENT_ID configuration option

#### NEXT STEPS FOR USER
1. Create a Google Cloud Project for the deployed domain
2. Set up OAuth 2.0 Web application credentials
3. Set GOOGLE_CLIENT_ID environment variable with the Web client ID before building/deploying
4. The Google sign-in button will appear automatically once configured

#### DOCUMENTATION REFERENCES
- docs/deployment.md: "To enable Google sign-in, set `GOOGLE_CLIENT_ID` to the OAuth 2.0 Web client ID..."
- .env.example: Shows optional GOOGLE_CLIENT_ID configuration
- backend: GoogleIdTokenIdentityVerifier and GoogleIdentityVerifier classes
- frontend: AuthView.vue shows conditional rendering based on googleConfigured

#### PROOF
Implementation verified in commit: 3285209
Google auth fully functional - ready for user configuration with real Google Client ID
