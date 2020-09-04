<template>
	<div
		class="card card-item"
		:data-id="card_id"
		:class="{
      'card--selected': this.selected,
      'card--disabled': this.card.is_ended,
    }"
	>
		<div class="card__content" @click="selected = !selected">
			<div class="border-line"></div>
			<div class="content__text">
				<p class="sub-title" data-text="Сказочное заморское яство" data-hover-text="Котэ не одобряет?"></p>
				<h3>Нямушка</h3>
				<h4>{{ card.taste }}</h4>
				<p>
					<b>{{ card.servings }}</b>
					{{ servingsCount }}
				</p>
				<p>
					<b v-if="card.gift != 1">{{ card.gift }}</b>
					{{ giftCount }}
					в подарок
				</p>
				<p v-if="card.is_ended">заказчик доволен</p>
			</div>

			<img class="photo-img" src="@/assets/cat-photo.png" alt="cat photo" />
			<div class="weight">
				<p class="weight-value">{{ card.weight }}</p>
				<p>кг</p>
			</div>
		</div>
		<p
			v-if="card.is_ended"
			class="description description-disabled"
		>Печалька, {{ card.taste }} закончился.</p>
		<p v-else-if="selected" class="description">{{ card.description }}</p>
		<p v-else class="description">
			Чего сидишь? Порадуй котэ,
			<a @click="selected = true" class="link">купи.</a>
		</p>
	</div>
</template>

<script>
export default {
	name: "Card",
	props: {
		card_id: Number,
		card: Object,
	},
	data() {
		return {
			selected: false,
		};
	},
	computed: {
		giftCount() {
			const lastNum = this.card.gift.substr(-1);
			if (lastNum == 1) return "мышь";
			else if (lastNum < 5 && lastNum != 0) return "мыши";
			else return "мышей";
		},
		servingsCount() {
			const lastNum = this.card.servings.substr(-1);
			if (lastNum == 1) return "порция";
			else if (lastNum < 5 && lastNum != 0) return "порции";
			else return "порций";
		},
	},
};
</script>

<style lang="scss" scoped>
$main-color: #1698d9;
$select-color: #d91667;
$corner-size: 50px;

.card {
	min-width: 321px;
	width: 321px;
	position: relative;
}

.card--disabled {
	pointer-events: none;
	user-select: none;
	.card__content {
		border-color: #b3b3b3;
		> * {
			filter: opacity(0.3);
		}
		.border-line {
			background-color: #b3b3b3;
			filter: opacity(0.7);
		}
	}
}

.card--selected {
	.card__content {
		border-color: $select-color;
	}
	.border-line {
		background-color: $select-color !important;
	}
	.weight {
		background-color: $select-color;
	}

	&:hover {
		.sub-title {
			color: $select-color;
			&::before {
				content: attr(data-hover-text);
			}
		}
	}
}

.card__content {
	min-height: 480px;
	background-color: #f2f2f2;
	padding-left: 48px;
	box-sizing: border-box;
	border-radius: 10px;
	border: 4px solid $main-color;
	display: flex;
	flex-direction: column;
	position: relative;
	overflow: hidden;
	clip-path: polygon(
		100% 0%,
		$corner-size 0%,
		0% $corner-size,
		0% 100%,
		100% 100%
	);
	.border-line {
		position: absolute;
		display: block;
		top: 0;
		left: 0;
		content: "";
		width: 100%;
		height: 100%;
		clip-path: polygon(0 0%, $corner-size 0, 0 $corner-size, 0% 0);
		background-color: $main-color;
	}

	.sub-title {
		font-size: 16px;
		margin: 20px 0 5px;
		&:before {
			content: attr(data-text);
		}
	}
	h3 {
		font-size: 48px;
		margin: 0;
	}
	h4 {
		margin-top: 0;
		margin-bottom: 15px;
		font-size: 24px;
	}
	p {
		margin: 0;
		font-size: 14px;
		line-height: 16px;
	}
}

.content__text {
	text-align: left;
}

.weight {
	position: absolute;
	bottom: 5px;
	right: 5px;
	width: 81px;
	height: 81px;
	border-radius: 50%;
	background-color: $main-color;
	display: flex;
	flex-direction: column;
	justify-content: center;

	&-value {
		font-size: 42px !important;
		line-height: 42px !important;
	}
	p {
		margin: 0;
		padding: 0;
		color: #fff;
		font-size: 21px;
		line-height: 22px;
	}
}

.photo-img {
	position: absolute;
	bottom: -4px;
	left: -4px;
}

.link {
	color: $main-color;
	border-bottom: dashed 1px $main-color;
	cursor: pointer;
}

.description {
	font-size: 13px;
	color: #fff;

	&-disabled {
		color: #ffff66;
	}
}
</style>
