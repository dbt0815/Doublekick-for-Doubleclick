// ==UserScript==
// @name         Block Google Cross-Site Tracking
// @namespace    
// @version      1.0
// @description  Block cross-site tracking by Google services (e.g., doubleclick.net, google-analytics.com).
// @author       dbt0815
// @match        *://*/*
// @grant        none
// @run-at       document-start
// ==/UserScript==

(function() {
    'use strict';

    // List of Google tracking domains to block
    const blockedDomains = [
        'doubleclick.net',
        'google-analytics.com',
        'googletagmanager.com',
        'googleadservices.com',
        'googlesyndication.com',
        'g.doubleclick.net',
        'pagead2.googlesyndication.com',
        'www.googleadservices.com',
        'adservice.google.com',
        'adservice.google.fr',
        'adservice.google.de',
        'adservice.google.co.uk',
        'adservice.google.es',
        'adservice.google.it',
        'adservice.google.nl',
        'adservice.google.se',
        // Add more Google tracking domains as needed
    ];

    // Convert the list to a set for efficient lookups
    const blockedDomainSet = new Set(blockedDomains);

    // Block requests to these domains
    const blockRequest = (details) => {
        const url = new URL(details.url);
        const domain = url.hostname.replace('www.', '');
        if (blockedDomainSet.has(domain)) {
            console.log(`Blocked request to: ${details.url}`);
            return { cancel: true };
        }
        return { cancel: false };
    };

    // Use the browser's webRequest API to block requests
    if (typeof browser !== 'undefined' && browser.webRequest) {
        browser.webRequest.onBeforeRequest.addListener(
            blockRequest,
            { urls: ["<all_urls>"] },
            ["blocking"]
        );
    } else if (typeof chrome !== 'undefined' && chrome.webRequest) {
        chrome.webRequest.onBeforeRequest.addListener(
            blockRequest,
            { urls: ["<all_urls>"] },
            ["blocking"]
        );
    }

})();
