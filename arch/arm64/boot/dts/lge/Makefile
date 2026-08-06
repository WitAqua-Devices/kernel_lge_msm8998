# Per Platform
ifeq ($(CONFIG_MACH_MSM8998_LUCY),y)
DTS_PROJECT := msm8998-lucy
endif
ifeq ($(CONFIG_MACH_MSM8998_JOAN),y)
DTS_PROJECT := msm8998-joan
endif

# Per Device
ifeq ($(CONFIG_MACH_MSM8998_LUCY_KR),y)
DTS_TARGET := msm8998-lucy_kr
endif
ifeq ($(CONFIG_MACH_MSM8998_LUCY_DCM_JP),y)
DTS_TARGET := msm8998-lucy_dcm_jp
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_KR),y)
DTS_TARGET := msm8998-joan_kr
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_VZW),y)
DTS_TARGET := msm8998-joan_vzw
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_ATT_US),y)
DTS_TARGET := msm8998-joan_att_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_SPR_US),y)
DTS_TARGET := msm8998-joan_spr_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_NAO_US),y)
DTS_TARGET := msm8998-joan_nao_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_TMO_US),y)
DTS_TARGET := msm8998-joan_tmo_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_CLR_PR),y)
DTS_TARGET := msm8998-joan_tmo_us
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_GLOBAL_COM),y)
DTS_TARGET := msm8998-joan_global_com
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_GLOBAL_CA),y)
DTS_TARGET := msm8998-joan_global_ca
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_ACG_US),y)
DTS_TARGET := msm8998-joan_acg_us
endif

# The two japanese SKUs accumulate rather than overwrite: one build serves
# both, and the bootloader picks the matching appended DTB by board id. The
# config symbols only ever reach this file and two `KDDI_JP || DCM_JP` guards
# that are already satisfied by either, so turning both on changes nothing but
# which device trees get built.
ifeq ($(CONFIG_MACH_MSM8998_JOAN_KDDI_JP),y)
DTS_TARGET += msm8998-joan_kddi_jp
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_DCM_JP),y)
DTS_TARGET += msm8998-joan_dcm_jp
endif

ifeq ($(CONFIG_MACH_MSM8998_JOAN_GLOBAL_LDU),y)
DTS_TARGET := msm8998-joan_global_ldu
endif

ALL_DTS := $(notdir $(wildcard $(addsuffix /*.dts,\
		$(addprefix $(srctree)/$(src)/$(DTS_PROJECT)/,$(DTS_TARGET)))))
dtb-y += $(patsubst %.dts,%.dtb,$(ALL_DTS))

DTB_NAMES := $(subst $\",,$(CONFIG_BUILD_ARM_APPENDED_DTB_IMAGE_NAMES))
ifneq ($(DTB_NAMES),)
DTB_LIST := $(addsuffix .dtb,$(DTB_NAMES))
else
DTB_LIST := $(dtb-y)
endif

always  := $(addprefix ../,$(DTB_LIST))

# One rule per target, since the prerequisite path cannot hold a list. Make
# picks whichever rule finds its .dts, and with a single target this is the
# rule that was here before.
define dts_target_rule
$(obj)/../%.dtb: $(src)/$(DTS_PROJECT)/$(1)/%.dts FORCE
	$$(call if_changed_dep,dtc)
endef

$(foreach t,$(DTS_TARGET),$(eval $(call dts_target_rule,$(t))))

clean-files := *.dtb
