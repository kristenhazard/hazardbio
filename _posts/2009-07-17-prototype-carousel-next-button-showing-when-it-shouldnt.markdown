---

layout: post
title: Carousel
published: false
topics: ajax prototype carousel rails

---

updateNextButton: function() {
  var lastPosition = this.currentLastPosition();
  var size = this.currentSize();
  var nextClassName = "next_button" + this.options.disabledButtonSuffix;

  if (this.nextButton.hasClassName(nextClassName) && lastPosition != size) {
    this.nextButton.removeClassName(nextClassName);
    this.fire('nextButton:enabled');
  }
  if (!this.nextButton.hasClassName(nextClassName) && lastPosition <= size) {
    this.nextButton.addClassName(nextClassName);
    this.fire('nextButton:disabled');
  }
},


if (!this.nextButton.hasClassName(nextClassName) && lastPosition == size) {
  
if (!this.nextButton.hasClassName(nextClassName) && lastPosition <= size) {