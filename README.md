# TAPSSKIP
SFL TAPS Skip
  HOW TO USE:
1. Open the traning website.
2. Enter your Name and what knot
3. Open the moudle you need to get done
4. Click "GO" to open the moudel
5. When the new window open, click into the moudel
6. Right click and open  "inspect"
7. Click console
8. Paste the "CONSOLE_CODE"
9. Close the windows and now that part is complected.
10. Repeat till done

CONSOLE_CODE


(function() {
   // First, try to find the SCORM API (SCORM 1.2)
   var API = window.API || window.parent.API || window.top.API;

   // If SCORM 1.2 API is not found, try to find SCORM 2004 API
   if (!API) {
       API = window.API_1484_11 || window.parent.API_1484_11 || window.top.API_1484_11;
   }

   // Check if the API is available
   if (!API) {
       console.error('SCORM API not found.');
       return;
   }

   // Function to mark the lesson as completed
   function markLessonAsCompleted() {
       try {
           var result = API.LMSSetValue("cmi.core.lesson_status", "completed");
           if (result) {
               var commitResult = API.LMSCommit("");
               if (commitResult) {
                   console.log('Lesson marked as completed.');
               } else {
                   console.error('Failed to commit the completion status.');
               }
           } else {
               console.error('Failed to set lesson status to completed.');
           }
       } catch (error) {
           console.error('Error reporting completion:', error);
       }
   }

   markLessonAsCompleted();

   setTimeout(function() {
       function checkSCORMAPI() {
           var API = window.API || window.parent.API || window.top.API;
           if (!API) {
               API = window.API_1484_11 || window.parent.API_1484_11 || window.top.API_1484_11;
           }
           if (API) {
               console.log('SCORM API found:', API);
               return API;
           } else {
               console.error('SCORM API not found.');
               return null;
           }
       }

       function initializeSCORM(API) {
           try {
               var result;
               if (API.LMSInitialize) {
                   result = API.LMSInitialize("");
                   if (result === "false") {
                       console.error('SCORM initialization failed.');
                       return false;
                   }
               }
               if (API.Initialize) {
                   result = API.Initialize("");
                   if (result === "false") {
                       console.error('SCORM initialization failed.');
                       return false;
                   }
               }
               console.log('SCORM initialized successfully.');
               return true;
           } catch (error) {
               console.error('Error during SCORM initialization:', error);
               return false;
           }
       }

       function markLessonAsCompleted(API) {
           try {
               if (!initializeSCORM(API)) {
                   return;
               }
               var result = API.LMSSetValue("cmi.core.lesson_status", "completed");
               console.log('LMSSetValue result:', result);
               if (result) {
                   var commitResult = API.LMSCommit("");
                   console.log('LMSCommit result:', commitResult);
                   if (commitResult) {
                       console.log('Lesson marked as completed.');
                   } else {
                       console.error('Failed to commit the completion status.');
                   }
               } else {
                   console.error('Failed to set lesson status to completed.');
               }
           } catch (error) {
               console.error('Error marking the lesson as completed:', error);
           }
       }

       var api = checkSCORMAPI();
       if (api) {
           markLessonAsCompleted(api);
       }
   }, 1500);
})();  
