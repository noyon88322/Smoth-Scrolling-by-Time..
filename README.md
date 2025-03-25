# Smoth-Scrolling-by-Time..
### recetnt time er item middle a asbe.

```bash

       // Find the position of the most recent item (i.e., today's or the closest upcoming date)
        int mostRecentIndex = -1;
        for (int i = 0; i < list.size(); i++) {
            try {
                Date modelDate = sdf.parse(list.get(i).getEnglishdate());
                Date currentDate = sdf.parse(currentDateStr);

                if (modelDate.equals(currentDate) || modelDate.after(currentDate)) {
                    mostRecentIndex = i;
                    break;  // Found the most recent item, no need to check further
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

        // Smoothly scroll to the most recent item and center it
        if (mostRecentIndex != -1) {
            int finalMostRecentIndex = mostRecentIndex;
            recylerviewpuja.post(new Runnable() {
                @Override
                public void run() {
                    // Get the LinearLayoutManager
                    LinearLayoutManager layoutManager = (LinearLayoutManager) recylerviewpuja.getLayoutManager();

                    if (layoutManager != null) {
                        // Create a LinearSmoothScroller for smoother scrolling
                        LinearSmoothScroller smoothScroller = new LinearSmoothScroller(getApplicationContext()) {
                            @Override
                            protected int getVerticalSnapPreference() {
                                return SNAP_TO_START;  // Use SNAP_TO_START or SNAP_TO_CENTER
                            }
                        };

                        // Set the target position (most recent item)
                        smoothScroller.setTargetPosition(finalMostRecentIndex);

                        // Start the smooth scroll
                        layoutManager.startSmoothScroll(smoothScroller);
                    }
                }
            });
        }

```
