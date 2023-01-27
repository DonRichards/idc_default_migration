INTRODUCTION
------------
The idc_default_migration module demonstrates how to implement custom migrations
for Drupal 8+. It includes:
* The main menu of library links

RUNNING THE MIGRATIONS
----------------------
The migrate_tools module (https://www.drupal.org/project/migrate_tools) provides
the tools you need to perform migration processes. At this time, the web UI only
provides status information - to perform migration operations, you need to use
the drush commands.

# Enable the tools and the example module if you haven't already.
drush en -y migrate_tools,idc_default_migration

# Look at the migrations. Just look at them. Notice that they are displayed in
# the order they will be run, which reflects their dependencies. For example,
# because the node migration references the imported terms and users, it must
# run after those migrations have been run.
drush ms               # Abbreviation for migrate-status

# Run the import operation for all the beer migrations.
drush migrate:import idc_default_migration_menu_link_main  # Abbreviation for migrate-import

# Look at what you've done! Also, visit the site and see the imported content,
# user accounts, etc.
drush ms

# Look at the duplicate import message.
drush mmsg idc_default_migration_menu_link_main   # Abbreviation for migrate-messages

drush mr idc_default_migration_menu_link_main  # Abbreviation for migrate-rollback

# Migrate by the group
drush migrate:import --group=idc

# Debugging and trying again
drush migrate:import idc_default_migration_menu_link_main
cp web/modules/contrib/idc_default_migration/migrations/migrate_plus.migration.idc_default_migration_menu_link_main.yml config/sync/ && drush config:import -y
drush migrate:rollback idc_default_migration_menu_link_main

# If there's a problem with the config and you need it removed.
drush config:delete migrate_plus.migration.idc_default_migration_menu_link_main
