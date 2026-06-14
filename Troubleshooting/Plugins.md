# Troubleshooting Crashes or Plugin Issues

Plugins can sometimes cause crashes, broken quests, missing UI, save problems, or other strange in-game behavior. This can happen after installing a new plugin, updating a plugin, changing your load order, or continuing an older save after plugins have changed.

Use the steps below to help narrow down which plug may be causing the problem.

## First, test with a new game

Start a new game and check whether the issue still happens.

- If the issue does not happen on a new game, your current save may still have old plugin data in it. In Starfield, you may need to go through Unity before the issue is fully cleared from that save.
- If the issue still happens on a new game, one of your installed plugins is probably causing the problem.

## Find the problem plugin

The goal is to disable your plugins, then turn them back on in small groups until the issue returns.

1. Create a new full save
   - Make a normal manual save before changing anything.
   - Do not use a quick save or auto save, because those can be overwritten.
   - You will use this save later after finding the problem plugin. It also helps preserve your current load order.

2. Disable all plugins
   - Turn off all plugins so you can test from a clean setup.

3. Re-enable plugins in small groups
   - Turn your plugins back on in small batches, around 5 at a time.
   - After enabling each batch, launch the game and test the issue.
   - If the problem comes back, one of the plugins in that batch is probably causing it.
   - If the problem does not come back, enable the next batch and test again.

4. Test the bad batch one plugin at a time
   - Once you find the batch that causes the issue, disable that batch again.
   - Then enable those plugins one at a time and test after each one.
   - When the issue comes back, you have likely found the problem plugin.

5. Restore your save and load order
   - After finding the broken plugin, enable the rest of your plugins again.
   - Load the full save you created in step 1.
   - When prompted, choose to use the saved game load order.
   - If the game warns that the broken plugin is missing, accept the warning. Do not let the game try to download or reinstall that plugin.

6. Test again
   - Once the broken plugin is removed, test the issue again.
   - If the problem is gone, you should be able to keep playing.
   - If the game still crashes or behaves strangely, your save may still contain old plugin data. In Starfield, going through Unity may be needed to fully clean up the save.

## What if the issue never comes back?

If you re-enable every plugin and the issue does not return, the problem may have been caused by load order or a plugin conflict rather than one specific broken plugin.

Those issues are harder to fix. You may need a compatibility patch, a different load order, or to remove one of the conflicting plugins.
