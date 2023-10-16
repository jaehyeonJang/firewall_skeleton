# @@@LICENSE
#
# Copyright (c) 2022 LG Electronics, Inc.
#
# Confidential computer software. Valid license from LG required for
# possession, use or copying. Consistent with FAR 12.211 and 12.212,
# Commercial Computer Software, Computer Software Documentation, and
# Technical Data for Commercial Items are licensed to the U.S. Government
# under vendor's standard commercial license.
#
# LICENSE@@@

file (READ base.in common_base_rule)
file (READ whitelist_static.in common_wl_rule)

configure_file(layout.in unknown.conf @only)
list (APPEND RULES ${CMAKE_CURRENT_BINARY_DIR}/unknown.conf)

# Configuration File
install (FILES ${RULES}
	DESTINATION /etc/firewall-manager/
	PERMISSIONS OWNER_WRITE OWNER_READ
	COMPONENT configurations
)
