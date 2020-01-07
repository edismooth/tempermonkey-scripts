// ==UserScript==
// @name         Azure DevOps collapsed ID
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       Oskar Gembalski
// @match        https://dev.azure.com/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    $('html').on('click', function(item) {
        if (item.target.className === 'expand-collapse-text') {
            let id = null;
            $('#taskboard-table-body tr').each(function() {
                if (this.id && this.id.indexOf('taskboard-row') === 0) {
                    id = $('#' + this.id).find('.id').first().text();
                } else {
                    const item = $('#' + this.id + ' .witTitle');
                    const textId = '[' + id + '] ';
                    if (item.text().indexOf(textId) !== 0) {
                        item.text(textId + item.text());
                    }
                }
            });
        }
    });
})();
